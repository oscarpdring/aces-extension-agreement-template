# Extension Agreement Generator

A DocAssemble interview system for generating License/Lease Extension & Modification Agreements with conditional sections and equipment modifications.

## Project Overview

This project creates professional extension agreements for laundry room licenses and leases with dynamic content based on user selections. The system uses conditional logic to include or exclude sections while maintaining proper numbering with "INTENTIONALLY OMITTED" entries for excluded sections.

## Features

### Core Functionality
- **Dynamic Agreement Generation**: Creates either License or Lease extension agreements
- **Conditional Sections**: Include/exclude sections based on business needs
- **Professional Formatting**: Maintains legal document numbering and structure
- **Multiple Document Types**: Supports various modification types

### Conditional Sections
- **Term Extensions**: Modify lease/license expiration dates
- **Equipment Modifications**: Handle equipment removal, installation, and upgrades
- **Rent Modifications**: Percentage rent calculations and fixed schedules
- **Compensation Changes**: Minimum compensation and rate increases
- **Improvements**: Tenant improvement requirements
- **Tax Modifications**: Real estate tax escalation changes

### User Experience Features
- **Choice Variables**: Select between License/Lease, Licensor/Lessor, Licensee/Lessee
- **Conditional Forms**: Questions appear based on previous selections
- **Rich Email Templates**: Comprehensive summaries with interactive checklists
- **Document Attachments**: PDF and Word format outputs

## Technical Architecture

### File Structure
- **extension_agreement_generator.yml**: Main interview file
- **config.yml**: Project metadata and dependencies
- **authentication.yml**: User access control
- **modules.yml**: Required dependencies
- **questions.yml**: All user input forms
- **initialize_all_var.yml**: Variable processing and calculations
- **email_function.yml**: Email template and sending functionality
- **summary.yml**: Interview summary generation
- **attaching_mandatory_docx.yml**: Document attachment configuration

### Utility Functions
- **number_to_words.yml**: Number to words conversion for legal documents
- **rent_schedule_generator.yml**: Dynamic rent schedule creation
- **set_tagging.yml**: Session management

### Dependencies
- **DocAssemble**: Core interview platform
- **num2words**: Number to words conversion
- **docassemble.base.util**: Base DocAssemble utilities

## Variable Architecture

### Core Variables
- **Agreement Information**: Date, parties, premises address
- **Choice Variables**: Agreement type, party roles
- **Financial Data**: Rent amounts, compensation rates, percentages
- **Dates**: Extension dates, effective dates, tax periods
- **Descriptive Content**: Equipment details, improvement work

### Formatted Variables
- **Currency Formatting**: All amounts include _decimal variants (e.g., $1,234.56)
- **Word Conversion**: Numbers include _words variants for legal text
- **Conditional Text**: Dynamic content based on user selections

### Boolean Logic
- All conditional decisions use _yn variables
- Nested conditionals for complex scenarios
- Proper handling of false conditions with "INTENTIONALLY OMITTED"

## Installation

### Prerequisites
- DocAssemble installation
- Access to DocAssemble playground or server
- Word document template support

### Setup Steps
1. **Upload Files**: Upload all .yml files to DocAssemble playground
2. **Template File**: Convert markdown template to .docx format
3. **Template Upload**: Place extension_agreement_template.docx in templates folder
4. **Main Interview**: Set extension_agreement_generator.yml as primary interview
5. **Dependencies**: Ensure num2words package is available

### Template Conversion
1. Copy content from aceslaundry extension agreement template.md
2. Paste into Microsoft Word
3. Format as needed (headers, spacing, fonts)
4. Save as extension_agreement_template.docx
5. Upload to DocAssemble templates directory

## Usage

### Starting an Interview
1. Access the Extension Agreement Generator interview
2. Log in when prompted (authentication required)
3. Complete all required fields
4. Review conditional sections
5. Generate documents

### Question Flow
1. **Basic Information**: Agreement details and parties
2. **Agreement Type Selection**: License vs Lease, party roles
3. **Conditional Sections**: Select applicable modifications
4. **Detail Entry**: Provide specific information for selected sections
5. **Review and Generate**: Create final documents

### Output Options
- **PDF Documents**: Professional formatted agreements
- **Word Documents**: Editable format for further modifications
- **Email Delivery**: Send documents with comprehensive summary
- **Interview Summary**: Detailed record of all responses

## Email Features

### Comprehensive Summary
- Agreement details and party information
- All modification sections with status
- Financial terms and calculations
- Equipment modification details
- Improvement and tax information

### Interactive Checklists
- Equipment removal/installation tasks
- Agreement execution requirements
- System updates and file management
- Conditional items based on selections

### Professional Format
- Structured HTML layout
- Clear section organization
- Checkbox forms for task tracking
- Document attachment list

## Conditional Logic

### Section Numbering
- Maintains sequential numbering (1.1, 1.2, 1.3, etc.)
- "INTENTIONALLY OMITTED" for excluded sections
- Preserves professional document structure
- No gaps in numbering sequence

### Equipment Modifications
- Main conditional: Include equipment modifications
- Sub-conditionals: Removal, installation, upgrade options
- Detailed descriptions for each selected type
- Professional formatting in final document

### Financial Modifications
- Percentage rent calculations with breakpoints
- Fixed rent schedules with annual amounts
- Minimum compensation guarantees
- Rate increase specifications

## Development Notes

### Directive Compliance
- Follows established DocAssemble architecture patterns
- Uses standard variable naming conventions
- Implements 7-step processing pattern
- Maintains proper file organization

### Code Organization
- Modular design with separate utility functions
- Clear separation of concerns
- Reusable components for similar projects
- Comprehensive error handling

### Testing Recommendations
- Test all conditional combinations
- Verify "INTENTIONALLY OMITTED" formatting
- Check email template functionality
- Validate document generation in multiple formats

## Support and Maintenance

### Common Issues
- Template variable mismatches: Verify all template variables exist in code
- Conditional logic errors: Check boolean variable definitions
- Email delivery problems: Verify SMTP configuration
- Document formatting: Check .docx template formatting

### Updating Templates
1. Modify markdown template file
2. Update corresponding variables in questions.yml
3. Adjust initialize_all_var.yml processing
4. Test conditional logic thoroughly
5. Update email template as needed

### Adding New Sections
1. Add boolean variable to questions.yml
2. Include conditional logic in initialize_all_var.yml
3. Update template with new section
4. Add "INTENTIONALLY OMITTED" handling
5. Update email template summary

## Version Information

- **Version**: 1.0
- **Release Date**: 2024-12-19
- **Author**: ACES Laundry Services
- **DocAssemble Compatibility**: Current stable release
- **Template Format**: Microsoft Word .docx

## License and Usage

This software is proprietary to ACES Laundry Services. Unauthorized reproduction or distribution is prohibited.

