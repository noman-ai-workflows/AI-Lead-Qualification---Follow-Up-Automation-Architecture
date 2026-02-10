function validateRequest(payload):

ensure payload has: - event - source - lead object

ensure lead has: - name - email - message

if any required field missing:
return invalid with error message

return valid
