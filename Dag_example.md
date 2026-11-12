```lua
local DAG = {}
DAG.__index = DAG

function DAG.new()
    return setmetatable({
        nodes = {},      -- [id] = payload (any value or entity ref)
        forward = {},    -- [id] = { [dependent_id] = true }
        in_degree = {},  -- [id] = count of unmet dependencies
    }, DAG)
end

function DAG:add_node(id, payload)
    if not self.nodes[id] then
        self.nodes[id] = payload or true
        self.forward[id] = {}
        self.in_degree[id] = 0
    end
    return self
end

-- Edge: `dep_id` must complete BEFORE `target_id` can start
function DAG:add_edge(dep_id, target_id)
    self:add_node(dep_id)
    self:add_node(target_id)
    if not self.forward[dep_id][target_id] then
        self.forward[dep_id][target_id] = true
        self.in_degree[target_id] = self.in_degree[target_id] + 1
    end
    return self
end

-- Returns a list of node IDs with 0 unmet dependencies
function DAG:get_ready(predicate)
    local ready = {}
    for id, deg in pairs(self.in_degree) do
        if deg == 0 and (not predicate or predicate(id, self.nodes[id])) then
            ready[#ready + 1] = id
        end
    end
    return ready
end

-- Marks a node finished and decrements in-degree of downstream dependents
function DAG:complete(id)
    if not self.nodes[id] then return end
    for dependent_id in pairs(self.forward[id]) do
        self.in_degree[dependent_id] = self.in_degree[dependent_id] - 1
    end
    self.nodes[id] = nil
    self.forward[id] = nil
    self.in_degree[id] = nil
end

return DAG
```
