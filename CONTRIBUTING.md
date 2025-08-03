# Contributing to BA_CyberRange_PoC

Thank you for your interest in contributing to this cyber range project! This document provides guidelines for contributing.

## Development Guidelines

### Code Style
- Use consistent indentation (2 spaces for YAML)
- Follow Ansible best practices
- Use descriptive variable names
- Add comments for complex logic

### Adding New PoCs
1. Create a new role directory under `roles/pocX/`
2. Follow the existing phase structure:
   - `reconnaissance/`
   - `initial-access/`
   - `privilege-escalation/`
   - `persistence/`
   - `action-on-objectives/`
3. Use variables instead of hardcoded values
4. Add error handling with `failed_when: false`

### Variable Management
- Add new variables to `group_vars/all.yml`
- Use descriptive variable names
- Document variables with comments
- Keep credentials centralized

### Testing
- Test playbooks in isolated environments
- Verify all phases execute correctly
- Check error handling works as expected
- Validate variable substitution

### Security Considerations
- This is for educational purposes only
- Use weak credentials only in isolated environments
- Document security implications clearly
- Follow responsible disclosure practices

## Pull Request Process
1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request with clear description

## Questions?
Contact the maintainer for any questions about contributing. 