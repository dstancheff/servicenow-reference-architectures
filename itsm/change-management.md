C4Context
title Change Management in ServiceNow - Extended Context Diagram with Risk Assessment

Person(User, "Change Requester", "A user requesting or reviewing a change")
Person(Change Manager, "Change Manager", "A user responsible for approving or rejecting changes")
Person(Change Advisory Board, "Change Advisory Board", "A group of people who run formal CAB meetings")


System_Boundary(SN, "ServiceNow Platform") {

  Container(CM, "Change Management", "Manages and approves changes")

  Container_Boundary(CM1, "Change Management") {
    Component(CPFC, "Change Process Flow")
    Boundary(CPF, "Change Process Flow") {
      Component(FD, "Flow Designer", "Automates business logic")
      Component(RA, "Risk Assessment", "Evaluates and manages change-related risks")
      Component(CForm, "Change Form", "Content page","Form layout, configuring fields, etc.")
      Component(UI Policy, "UI Policy", "Enforces visibility, mandatory and read-only rules")
      Component(UI Action, "UI Action", "Triggers server/client side logic")
      Component(CAB, "CAB Workbench", "Review and approval interface","Manage CAB meetings and decisions")
      Component(ApprovalPolicies, "Change Approval Policies", "Define approval rules","Configure approval workflows and routing")
      Component(ClientScr, "Client Script", "Client-side logic","Validation, field population, UI enhancements")
      Component(BR, "Business Rules", "Server-side logic","Approval workflows, routing rules, notifications")
      Component(SI, "Script Include", "Server-side logic","Reusable code for validation and notifications")
      Component(GR, "GlideRecord", "JavaScript API","Access to change-related data")
      Component(SJ, "Scheduled Job", "Server-side logic","Automate notifications and escalations")
      Component(Notify, "Notifications", "Notification","Change notifications for approvals, escalations, implementations")
      Component(Properties, "Properties", "Application properties","Control CM features, approvals, notifications")
      Rel(CForm, UI Policy, "Uses")
      Rel(CForm, UI Action, "Uses")
      Rel(CForm, UI Policy, "Uses")
      Rel(CForm, UI Action, "Uses")
      Rel(CForm, ClientScr, "Triggers")
      Rel(BR, SI, "Uses")
      Rel(BR, GR, "Uses")
      Rel(BR, CMDB, "Reads/Updates")
      Rel(SJ, BR, "Executes")
      Rel(SJ, SI, "Executes")
      Rel(SJ, GR, "Executes")
      Rel(Notify, User, "Sends to")
      Rel(Notify, Change Manager, "Sends to")
      Rel(Properties, BR, "Consumes")
      Rel(Properties, SI, "Consumes")
      Rel(RA, User, "Communicates to")
      Rel(RA, Change Manager, "Communicates to")
      Rel(Change Advisory Board, CAB, "Uses")
      Rel(ApprovalPolicies, FD, "Uses")
    }
  }
}
System(CMDB, "Configuration Management Database", "Stores configuration and change-related data")
System(ES, "External Systems", "External systems and APIs interacting with Change Management")

Rel(User, CM, "Submits or reviews change requests")
Rel(Change Manager, CM, "Submits or reviews change requests")
Rel(CAB, CM, "Manages")
Rel(CM, CMDB, "Queries and updates change-related data")
UpdateLayoutConfig($c4ShapeInRow="4", $c4BoundaryInRow="1")