function processLead(rawRequest):

log = createExecutionLog()

log.add(
step = "Request",
status = "Success",
message = "Lead received",
details = rawRequest
)

validationResult = validateRequest(rawRequest)

if validationResult is invalid:
log.add(
step = "Validation",
status = "Rejected",
message = "Invalid lead payload",
details = validationResult.error
)
return failureResponse(log)

log.add(
step = "Validation",
status = "Success",
message = "Lead validated"
)

normalizedLead = normalizeLeadData(rawRequest)

log.add(
step = "Normalization",
status = "Success",
message = "Lead normalized",
details = normalizedLead
)

aiDecision = qualifyLeadWithAI(normalizedLead)

log.add(
step = "AI Qualification",
status = "Success",
message = "Lead classified by AI",
details = aiDecision
)

if aiDecision.action is not "ignore":

    storeLeadInCRM(normalizedLead, aiDecision)

    log.add(
      step = "CRM",
      status = "Success",
      message = "Lead stored with AI metadata"
    )

    emailResult = sendFollowUpEmail(
      to = normalizedLead.email,
      content = aiDecision.followUpEmail
    )

    if emailResult failed:
      log.add(
        step = "Email",
        status = "Error",
        message = "Email delivery failed",
        details = emailResult.error
      )
    else:
      log.add(
        step = "Email",
        status = "Success",
        message = "Follow-up email sent"
      )

else:
log.add(
step = "CRM & Email",
status = "Ignored",
message = "Lead not a fit"
)

persistLatestExecutionLog(log)

return successResponse(log)
