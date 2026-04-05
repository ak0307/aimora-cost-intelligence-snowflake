# Add a new API endpoint to AIMORA

## Requirements
- Add endpoint to `apps/api/` FastAPI backend
- Strongly type all request/response objects in TypeScript/Pydantic
- Include explicit error handling
- Document endpoint purpose and parameters
- Maintain backward compatibility where practical
- Add input validation
- Include appropriate HTTP status codes
- Consider caching strategy if needed

## Context
AIMORA API surfaces recommendations and telemetry data to the frontend. Each endpoint must:
1. Have clear, typed request/response contracts
2. Include proper error handling with meaningful messages
3. Handle edge cases (empty results, invalid params, permission denied)
4. Be idempotent where appropriate
5. Exclude internal implementation details from responses

## Steps
1. Define endpoint path and HTTP method (GET/POST/PUT)
2. Create Pydantic request model (with validation)
3. Create Pydantic response model
4. Implement endpoint handler with error handling
5. Add route to router configuration
6. Write validation/test cases
7. Update API documentation
8. Consider frontend integration needs

## Response Contract Template
```python
class EndpointResponse(BaseModel):
    status: str  # "success" | "error"
    data: Optional[dict] = None
    message: Optional[str] = None
    error_code: Optional[str] = None
```

## Validation Checklist
- [ ] Request/response types are explicit (no `any`)
- [ ] Error handling covers all edge cases
- [ ] Status codes are appropriate
- [ ] Documentation is clear
- [ ] Backward compatibility preserved
- [ ] Tests pass