# API + UI Integration Test

**Scenario:** 
- Create a project via API
- Verify project appears in Web UI
- Verify project is accessible on mobile
- Ensure tenant isolation (project visible only to the correct company)

**Assumptions:**
- API requires Bearer token and X-Tenant-ID
- Test data (project names) is unique per test run
- Mobile testing uses BrowserStack
- Cleanup of test projects is done after the test
## Test Strategy

1. **API Layer:** Use requests library to create a project and get project ID.
2. **Web UI Layer:** Use Playwright to log in, navigate to projects, and verify the project appears.
3. **Mobile Layer:** Use BrowserStack with Playwright to check project accessibility on mobile devices.
4. **Tenant Isolation:** Attempt to access project under a different tenant; should not be visible.
5. **Test Data Handling:** Dynamic project names; data stored in memory or JSON files for reuse.
6. **Edge Cases:** Network failures, slow UI load, mobile responsiveness.
## Pseudo-Code Example

def test_project_creation_flow():
    # 1. API: Create project
    project_id = create_project_via_api(project_name, tenant_id)
    
    # 2. Web UI: Verify project display
    login_web_ui(user)
    assert project_name is visible on projects page
    
    # 3. Mobile: Verify accessibility
    open_mobile_browser(device)
    assert project_name is visible
    
    # 4. Tenant Isolation
    switch_tenant(other_company)
    assert project_id is not visible
## Technical Decisions

- **Pytest**: lightweight, widely used for API and UI tests
- **Playwright**: handles web UI automation and mobile emulation
- **BrowserStack**: ensures cross-browser and mobile device coverage
- **JSON config**: centralizes environments, browsers, and test data
- **Dynamic test data**: avoids collisions and allows parallel tests
- **Tenant isolation checks**: ensures security boundaries
