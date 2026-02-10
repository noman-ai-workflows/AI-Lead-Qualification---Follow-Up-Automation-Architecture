function createExecutionLog():

logs = []

function add(step, status, message, details):
logs.push({
step,
status,
message,
details,
timestamp
})

function get():
return logs

return { add, get }
