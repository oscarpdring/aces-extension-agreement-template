# DocAssemble Project Architecture Directive
## **Master Template for Document Generation Interviews**

*Based on analysis of the highly successful Lease Agreement Generator project*

---

## **🚀 TEMPLATE-TO-INTERVIEW CONVERSION WORKFLOW**

### **PHASE 1: TEMPLATE ANALYSIS & VARIABLE EXTRACTION**

#### **Step 1.1: Document Template Analysis**
When provided with a document template (Word, PDF, etc.), follow this systematic approach:

1. **Extract All Variables** - Create comprehensive list of `{{ variable_name }}` placeholders
2. **Categorize Variables** - Group by data type and business logic
3. **Identify Patterns** - Look for related variables that suggest complex data structures
4. **Map Conditional Logic** - Find sections that should appear/disappear based on conditions
5. **Document Relationships** - Note calculated fields, derived values, and dependencies

#### **Step 1.2: Variable Conversion to Standard Patterns**
**CRITICAL:** Always convert template variables to match the established naming conventions:

```yaml
# Template Variable → Standard Convention Mapping Examples:
{{ client_name }} → {{ tenant_entity }}
{{ property_address }} → {{ building_complete_address }} 
{{ start_date }} → {{ lease_commencement_date }}
{{ has_broker }} → {{ broker_involved_yn }}
{{ broker_fee }} → {{ broker_commission }}
{{ total_deposit }} → {{ security_deposit_total_decimal }}
```

#### **Step 1.3: Variable Classification Checklist**
For each extracted variable, determine:
- [ ] **Input Type:** User input vs. calculated/derived
- [ ] **Data Type:** text, number, date, boolean, file, list
- [ ] **Conditionality:** Always shown vs. conditional on other variables
- [ ] **Formatting Needs:** Raw value vs. needs `_decimal`, `_words`, `_list` variants
- [ ] **Business Logic:** Simple field vs. complex calculation

---

## **PHASE 2: QUESTIONS.YML GENERATION**

### **Step 2.1: Questions Structure Template**
For ANY new interview, start with this exact structure:

```yaml
---
question: [Project Context] Information
fields:
 # BASIC INFORMATION SECTION
 - [Core Date Field]: [date_variable]
   datatype: date
 - [Primary Entity 1]: [entity1_variable]
   datatype: text
 - [Primary Entity 2]: [entity2_variable]
   datatype: text
   
 # BOOLEAN DECISION POINTS
 - "[Yes/No Question]?": [decision_yn]
   datatype: yesnoradio
 - [Conditional Field]: [conditional_variable]
   datatype: [appropriate_type]
   show if: [decision_yn]
   
 # FINANCIAL/NUMERIC FIELDS
 - [Amount Description] ($): [amount_variable]
   datatype: number
 - [Duration/Count]: [duration_variable]
   datatype: number
   
 # COMPLEX/LIST FIELDS
 - [Multi-line Description]: [description_variable]
   datatype: area
   help: |
     [Instructions for proper formatting]
 - [List of Items] (one per line): [list_variable]
   datatype: area
   help: |
     Enter each item on a separate line.
     Example:
     Item 1
     Item 2
     Item 3
     
 # FILE UPLOADS (if needed)
 - [File Description]: [file_variable]
   datatype: file
   required: false
   accept: |
     "image/jpeg, image/png, application/pdf"
   help: |
     [File upload instructions]
     
 # DOCUMENT CONTROL BOOLEANS
 - Would you like [Document Type A]?: [doc_a_yn]
   datatype: yesnoradio
   help: |
     [Description of when this document is needed]
 - Would you like [Document Type B]?: [doc_b_yn]
   datatype: yesnoradio
   help: |
     [Description of when this document is needed]
---
```

### **Step 2.2: Field Type Decision Matrix**
| Template Variable Pattern | Question Field Type | Standard Convention | Notes |
|---------------------------|-------------------|-------------------|-------|
| Names, addresses, descriptions | `datatype: text` | `[entity]_[attribute]` | - |
| Dollar amounts, quantities | `datatype: number` | `[concept]_amount` | - |
| Percentages | `datatype: decimal` | `[concept]_percentage` | For % values |
| Yes/No decisions (important) | `datatype: yesnoradio` | `[concept]_yn` | Use for major decisions |
| Yes/No decisions (simple) | `datatype: yesno` | `[concept]_yn` | Use for simple existence checks |
| Dates | `datatype: date` | `[event]_date` | - |
| Lists, multiple items | `datatype: area` | `[concept]_[descriptor]` | One item per line |
| File attachments | `datatype: file` | `[concept]_[type]` | Set required: false |

---

## **PHASE 3: INITIALIZE_ALL_VAR.YML CONSTRUCTION**

### **Step 3.1: The 7-Step Processing Pattern (MANDATORY)**
**Every new interview MUST follow this exact structure:**

```yaml
---
mandatory: True
code: |
 if not defined('user_approves'):

   
   # STEP 1: COLLECT ALL BASIC INPUTS
   need([primary_variable_1])
   need([primary_variable_2])
   need([primary_variable_3])
   # Type conversions
   [numeric_variable] = int([numeric_variable])
   [decimal_variable] = float([decimal_variable])
   
   # STEP 2: PROCESS CONDITIONAL LOGIC
   need([decision_variable_yn])
   if [decision_variable_yn]:
     need([conditional_variable_1])
     need([conditional_variable_2])
     # Calculate conditional values
     [derived_conditional] = [calculation_function]([inputs])
     [formatted_conditional] = f"${[derived_conditional]:,.2f}"
     [text_variation_1] = "[Template text with ] + [conditional_variable_1] + [more text]"
     [text_variation_2] = "[Alternative template text]"
   else:
     [conditional_variable_1] = "N/A"
     [conditional_variable_2] = 0
     [formatted_conditional] = "$0.00"
     [text_variation_1] = ""
     [text_variation_2] = ""
   
   # STEP 3: CALCULATE DERIVED VALUES
   # Currency formatting
   [amount_variable_decimal] = f"${[amount_variable]:,.2f}"
   # Word conversion
   [numeric_variable_words] = number_to_words([numeric_variable])
   # Mathematical calculations
   [calculated_total] = [base_amount] * [multiplier]
   [calculated_total_decimal] = f"${[calculated_total]:,.2f}"
   [calculated_total_words] = number_to_words([calculated_total])
   
   # STEP 4: PROCESS COMPLEX DATA (lists, schedules, etc.)
   if [data_type_decision_yn]:
     [complex_data_text] = create_[data_type]_schedule([parameters])
     [complex_data_html] = generate_[data_type]_html([parameters])
   else:
     need([custom_data_input])
     [complex_data_text] = create_[data_type]_schedule(
       [param1]=[value1],
       [param2]=[value2],
       [type]="custom",
       [custom_input]=[custom_data_input]
     )
     [complex_data_html] = generate_[data_type]_html([same_parameters])
   
   # List processing
   [entity_list_formatted] = format_[entity]_list([entity_input])
   [entity_comma_list] = format_comma_list([entity_input])
   
   # STEP 5: DATE CALCULATIONS
   [end_year] = ([start_date].year + [duration_years])
   [end_day] = [start_date].day
   [end_month] = [start_date].month
   [end_month_word] = num_to_month([end_month])
   [start_month_word] = num_to_month([start_date].month)
   
   # STEP 6: DOCUMENT SELECTION LOGIC
   need([doc_type_a_yn])
   need([doc_type_b_yn])
   need([doc_type_c_yn])
   
   docs_to_show = [[mandatory_doc_1], [mandatory_doc_2]]
   if [doc_type_a_yn]:
     docs_to_show.append([optional_doc_a])
   if [doc_type_b_yn]:
     docs_to_show.append([optional_doc_b])
   if [doc_type_c_yn]:
     docs_to_show.append([optional_doc_c])
   
   # STEP 7: COMPLETION FLAG
   need(session_tagging_complete)
   all_fields_complete = True
---
```

---

## **PHASE 4: EMAIL TEMPLATE CONSTRUCTION**

### **Step 4.1: Email Template Sections (MANDATORY STRUCTURE)**
**Every email template MUST include these sections in this order:**

```yaml
---
modules:
  - docassemble.base.util
---
code: |
  import os
  def format_document_list(docs):
    doc_names = []
    for doc in docs:
        if hasattr(doc, 'info'):
            doc_names.append(doc.info.get('name', 'Document'))
        elif hasattr(doc, 'filename'):
            doc_names.append(os.path.splitext(doc.filename)[0])
        else:
            doc_names.append('Document')
    return doc_names

  attachment_list = format_document_list(docs_to_show)

  def get_[entity]_list([entity]_text):
    if not [entity]_text:
        return []
    return [name.strip() for name in [entity]_text.split('\n') if name.strip()]

  individual_[entities] = get_[entity]_list([entity_variable])
  [entity]_comma_list = ', '.join(individual_[entities]) if individual_[entities] else 'None'
---
template: email_template
subject: |
  [Document Type] for ${[key_identifier_1]}, ${[key_identifier_2]}
content: |
  <strong><u>Date:</u></strong> ${today()}
  
  <strong><u>[PRIMARY ENTITY/LOCATION INFO]:</u></strong>
  <ul>
    <li>[Key Field 1]: ${[variable_1]}</li>
    <li>[Key Field 2]: ${[variable_2]}</li>
  </ul>
  
  <strong><u>[PARTIES/ENTITIES]:</u></strong>
  <ul>
    <li>[Entity 1]: ${[entity_1_variable]}</li>
    <li>[Entity 2]: ${[entity_2_variable]}</li>
    <li>[Entity 3]: ${[entity_3_variable]}</li>
  </ul>
  
  <strong><u>[CORE TERMS/VALUES]:</u></strong>
  <ul>
    <li>[Key Date]: ${[date_variable]}</li>
    <li>[Duration]: ${[duration_variable]}</li>
    <li>[Primary Amount]: ${[amount_variable_decimal]}</li>
    <li>[Secondary Amount]: ${[secondary_amount_decimal]}</li>
    <li>[Conditional Field]: ${[conditional_value] if [condition_yn] else "N/A"}</li>
  </ul>

  <strong><u>[COMPLEX DATA SCHEDULE/TABLE]:</u></strong>
  <ul>
    % for line in [complex_data_html].split('<br>'):
      % if line.strip():
        <li>${line}</li>
      % endif
    % endfor
  </ul>

  <strong><u>[CONDITIONAL SECTION] INFORMATION:</u></strong>
  <ul>
    <li>[Decision]: ${word(yesno([decision_yn]))}</li>
    <li>[Conditional Field]: ${[conditional_variable]}</li>
    <li>[Conditional Amount]: ${[conditional_amount_decimal] if [decision_yn] else "N/A"}</li>
  </ul>
  
  <strong><u>[DESCRIPTIVE/USE] INFORMATION:</u></strong>
  <ul>
    <li>[Description Field]: ${[description_variable]}</li>
    <li>[Additional Field]: ${[additional_variable]}</li>
  </ul>
  
  <strong><u>ADDITIONAL DOCUMENTS:</u></strong>
  <ul>
    <li>[Document A] Required: ${word(yesno([doc_a_yn]))}</li>
    <li>[Document B] Required: ${word(yesno([doc_b_yn]))}</li>
    <li>[Document C] Required: ${word(yesno([doc_c_yn]))}</li>
  </ul>
  
  <strong><u>[ENTITY LIST] INFORMATION:</u></strong>
  <ul>
    <li>[Entity List]: ${[entity_comma_list]}</li>
  </ul>
  
  <strong><u>ATTACHED FILES:</u></strong>
  <ul>
    % for name in attachment_list: 
      <li>${name}</li>
    % endfor
  </ul>

  % if individual_[entities]:
    % for i, [entity] in enumerate(individual_[entities]):
  <strong><u>[ENTITY] CHECKLIST - ${[entity].upper()}:</u></strong>
  <form>
    <div style="margin-left: 20px;">
      <input type="checkbox" id="[requirement_1]_${i}"> <label for="[requirement_1]_${i}">[Requirement 1 description]</label><br>
      <input type="checkbox" id="[requirement_2]_${i}"> <label for="[requirement_2]_${i}">[Requirement 2 description]</label><br>
      <input type="checkbox" id="[requirement_3]_${i}"> <label for="[requirement_3]_${i}">[Requirement 3 description]</label><br>
    </div>
  </form>
  <br>
    % endfor
  % endif

  <strong><u>[MAIN PROCESS] CHECKLIST:</u></strong>
  <form>
    <div style="margin-left: 20px;">
      <input type="checkbox" id="[main_req_1]"> <label for="[main_req_1]">[Main requirement 1]</label><br>
      <input type="checkbox" id="[main_req_2]"> <label for="[main_req_2]">[Main requirement 2]</label><br>
      <input type="checkbox" id="[main_req_3]"> <label for="[main_req_3]">[Main requirement 3]</label><br>
      % if [conditional_boolean]:
      <input type="checkbox" id="[conditional_req]"> <label for="[conditional_req]">[Conditional requirement]</label><br>
      % endif
    </div>
  </form>  
  
  Please retain this email for your records. These values can be used to recreate the documents if needed.
---
question: |
  Where should we send the documents?
fields:
  - Email: recipient_email
    datatype: email
---
question: |
  Documents Sent Successfully
subquestion: |
  Your documents have been sent to ${recipient_email}.
  All generated documents were included in the email.
event: email_sent
---
question: |
  Error Sending Documents
subquestion: |
  There was an error sending your documents to ${recipient_email}.
  Please try again or contact support if the problem persists.
event: email_error
```

---

## **PHASE 5: COMPLETE PROJECT ASSEMBLY**

### **Step 5.1: Mandatory File Creation Checklist**
For EVERY new project, create these files in exact order:

1. **config.yml** - Project metadata and dependencies
2. **authentication.yml** - Copy exactly from template (no changes needed)
3. **modules.yml** - Copy exactly from template (no changes needed)  
4. **questions.yml** - Built from Phase 2 analysis
5. **initialize_all_var.yml** - Built from Phase 3 pattern
6. **[utility_functions].yml** - Create as needed for calculations/formatting
7. **email_function.yml** - Built from Phase 4 template
8. **summary.yml** - Copy exactly from template (no changes needed)
9. **attaching_mandatory_docx.yml** - Configure for primary documents
10. **attach_[doc_type].yml** - One file per conditional document
11. **[main_interview].yml** - Include all modules and trigger logic

### **Step 5.1.1: Main Interview File Structure (EXACT PATTERN)**
```yaml
---
metadata: 
  title: |
     [Project Name] Generator

---
include:
  - authentication.yml 
  - modules.yml
  - config.yml
  - [utility_function_files].yml  # number_to_words.yml, format_comma_list.yml, etc.
  - initialize_all_var.yml        # CRITICAL: Variable processing hub
  - questions.yml                 # CRITICAL: All user questions
  - attaching_mandatory_docx.yml
  - attach_[document_type].yml    # One for each conditional document
  - summary.yml
  - email_function.yml
  - set_tagging.yml

---
code: | 
  if all_fields_complete:
    final_document
```

### **Step 5.2: Session Tagging Implementation**
**CRITICAL:** Every project needs session tagging. Create `set_tagging.yml`:

```yaml
---
code: |
  session_tagging_complete = True
---
```

This must be referenced in `initialize_all_var.yml` as `need(session_tagging_complete)`.

### **Step 5.3: Document Template Integration**
1. **Convert template to DOCX** if not already
2. **Replace all variables** with standard naming convention
3. **Add conditional logic** using Jinja2 syntax where needed
4. **Test variable mapping** against initialize_all_var.yml calculations

### **Step 5.4: Attaching_mandatory_docx.yml Structure (EXACT PATTERN)**
```yaml
---
mandatory: True
question: |
 Here is your document.
allow emailing: True
email template: email_template
attachment code: |
 docs_to_show
---
attachment:
 name: [Primary Document Name]
 filename: [Primary Document Name]
 docx template file: [primary_template].docx
 valid formats:
   - pdf
   - docx
 variable name: [primary_document_variable]
 
---
attachment:
 name: [Secondary Document Name]
 filename: [Secondary Document Name]
 docx template file: [secondary_template].docx
 valid formats:
   - pdf
   - docx
 variable name: [secondary_document_variable]
---
```

### **Step 5.5: Individual Attachment Files Pattern**
Each conditional document gets its own file: `attach_[document_type].yml`

```yaml
---
attachment:
 name: [Specific Document Name]
 filename: [Specific Document Name]
 docx template file: [specific_template].docx
 valid formats:
   - pdf
   - docx
 variable name: [specific_doc_variable]
---
```

---

## **⚡ QUICK START: TEMPLATE-TO-INTERVIEW CONVERSION**

### **When Given a New Document Template, Follow This Exact Process:**

#### **STEP 1: Variable Extraction (5-10 minutes)**
1. **Open the template document**
2. **Find all `{{ variable_name }}` placeholders**
3. **Create a list in this format:**
   ```
   EXTRACTED VARIABLES:
   - {{ client_name }} → user input, text
   - {{ service_date }} → user input, date  
   - {{ total_amount }} → user input, number
   - {{ has_warranty }} → user input, boolean
   - {{ warranty_terms }} → conditional on has_warranty, text
   - {{ formatted_total }} → derived from total_amount, currency
   ```

#### **STEP 2: Map to Standard Conventions (10-15 minutes)**
4. **Convert each variable to match the project's naming patterns:**
   ```
   VARIABLE MAPPING:
   {{ client_name }} → {{ client_entity }}
   {{ service_date }} → {{ service_commencement_date }}
   {{ total_amount }} → {{ service_total_amount }}
   {{ has_warranty }} → {{ warranty_included_yn }}
   {{ warranty_terms }} → {{ warranty_description }}
   {{ formatted_total }} → {{ service_total_amount_decimal }}
   ```

#### **STEP 3: Build Questions.yml (15-20 minutes)**
5. **Create questions.yml following the exact template structure**
6. **Group related fields logically**
7. **Add conditional `show if:` statements**
8. **Include proper help text with examples**

#### **STEP 4: Build Initialize_all_var.yml (20-30 minutes)**
9. **Follow the 7-step pattern exactly**
10. **Add all `need()` statements for user inputs**
11. **Implement conditional logic for optional fields**
12. **Calculate all derived values (`_decimal`, `_words`, etc.)**
13. **Set up document inclusion logic**

#### **STEP 5: Create Email Template (15-20 minutes)**
14. **Copy the email template structure exactly**
15. **Replace placeholder sections with project-specific content**
16. **Ensure all variables are properly referenced**
17. **Customize checklists for the specific business process**

#### **STEP 6: Configure Documents (10-15 minutes)**
18. **Update Word template with new variable names**
19. **Set up attachment files for each document type**
20. **Configure conditional document inclusion**

#### **STEP 7: Final Assembly (5-10 minutes)**
21. **Create main interview file with all includes**
22. **Add session tagging file**
23. **Test the complete workflow**

### **TOTAL TIME ESTIMATE: 1.5-2 hours for complete conversion**

---

## **🎯 PRACTICAL EXAMPLE: CONVERSION WORKFLOW**

### **Example: Converting a "Service Agreement" Template**

**Given template with variables:**
```
{{ client_name }}, {{ service_date }}, {{ total_cost }}, {{ has_warranty }}, {{ warranty_period }}
```

**Step 1: Standard Conversion**
```yaml
# Variables become:
client_entity            # Primary entity  
service_commencement_date # Key date
service_total_amount     # Financial amount
warranty_included_yn     # Boolean decision
warranty_duration_months # Conditional numeric field

# Derived variables automatically added:
service_total_amount_decimal    # Currency formatting
service_total_amount_words      # Number to words
warranty_duration_months_words  # Conditional number to words
```

**Step 2: Questions.yml Structure**
```yaml
---
question: Service Agreement Information
fields:
 - Service Date: service_commencement_date
   datatype: date
 - Client Entity Name: client_entity
   datatype: text
 - Total Service Cost ($): service_total_amount
   datatype: number
 - "Warranty Included?": warranty_included_yn
   datatype: yesnoradio
 - Warranty Duration (Months): warranty_duration_months
   datatype: number
   show if: warranty_included_yn
---
```

**Step 3: Initialize_all_var.yml Implementation**
```yaml
---
mandatory: True
code: |
 if not defined('user_approves'):
   # STEP 1: COLLECT INPUTS
   need(service_commencement_date)
   need(client_entity)
   need(service_total_amount)
   service_total_amount = int(service_total_amount)
   
   # STEP 2: CONDITIONAL LOGIC
   need(warranty_included_yn)
   if warranty_included_yn:
     need(warranty_duration_months)
     warranty_duration_months_words = number_to_words(warranty_duration_months)
   else:
     warranty_duration_months = 0
     warranty_duration_months_words = "zero"
   
   # STEP 3: DERIVED VALUES
   service_total_amount_decimal = f"${service_total_amount:,.2f}"
   service_total_amount_words = number_to_words(service_total_amount)
   
   # STEP 4-7: [Continue with pattern...]
   all_fields_complete = True
---
```

This example shows the exact mechanical process of conversion that will work for ANY template in ANY domain (legal, medical, business, etc.).

---

## **🏗️ PROJECT STRUCTURE OVERVIEW**

### **Core File Organization Pattern**
```
project_root/
├── [main_interview].yml          # Primary interview file (includes all modules)
├── config.yml                    # Project metadata and dependencies
├── authentication.yml            # User authentication and access control
├── modules.yml                   # External dependencies and imports
├── initialize_all_var.yml        # Central variable processing and calculations
├── questions.yml                 # All user input questions and form fields
├── email_function.yml            # Email template and sending functionality
├── summary.yml                   # Interview summary generation
├── attaching_mandatory_docx.yml  # Primary document attachments and email setup
├── attach_[document_type].yml    # Individual document attachment definitions
├── [utility_functions].yml       # Specific utility/formatting functions
└── [template_files].docx         # Word document templates
```

---

## **📋 MANDATORY IMPLEMENTATION REQUIREMENTS**

### **1. MAIN INTERVIEW FILE STRUCTURE**
```yaml
---
metadata: 
  title: |
     [Project Name] Generator

---
include:
  - authentication.yml 
  - modules.yml
  - config.yml
  - [utility_function_files].yml
  - initialize_all_var.yml    # CRITICAL: Variable processing hub
  - questions.yml             # CRITICAL: All user questions
  - attaching_mandatory_docx.yml
  - [attach_specific_docs].yml
  - summary.yml
  - email_function.yml
  # Add additional attachment files as needed

---
code: | 
  if all_fields_complete:
    final_document
```

### **2. CONFIG.YML STRUCTURE**
```yaml
---
metadata:
  title: [Project Name] Generator
  description: [Brief description of what the project generates]
  authors:
    - [organization/author]
  revision_date: [YYYY-MM-DD]
  version: [X.X]
  required_dependencies: 
    - num2words                    # For number-to-words conversion
    - docassemble.base.util       # Core DocAssemble utilities
  document_outputs:
    - [primary document name]
    - [secondary document name]
    - [additional rider/attachment names]
---
```

### **3. AUTHENTICATION.YML PATTERN**
```yaml
---
mandatory: True
code: |
  if not user_logged_in():
    need_unauthorized
  else:
    allowed_to_continue = True
---
question: |
  Unauthorized Access
event: need_unauthorized
subquestion: |
  You must be logged in to access this interview.
  
  Please use the "Sign in" button in the top right corner of the screen to log in or create an account.
---
```

### **4. MODULES.YML STRUCTURE**
```yaml
---
modules:
  - docassemble.base.util
  - num2words                     # Essential for number formatting
---
```

---

## **🔧 VARIABLE ARCHITECTURE STANDARDS**

### **A. NAMING CONVENTIONS (MANDATORY)**

#### **Core Data Categories:**
- **Parties:** `[entity_type]_[attribute]` (e.g., `landlord_entity`, `tenant_name`)
- **Dates:** `[event]_date` (e.g., `contract_date`, `commencement_date`)
- **Financial:** `[concept]_amount` or `[concept]_[unit]` (e.g., `initial_payment_amount`, `term_years`)
- **Booleans:** `[concept]_yn` (e.g., `broker_involved_yn`, `insurance_required_yn`)
- **Properties:** `[entity]_[property]_[descriptor]` (e.g., `building_complete_address`)

#### **Derived Variable Patterns:**
- **Currency formatting:** `[base_name]_decimal` (e.g., `total_amount_decimal`)
- **Word conversion:** `[base_name]_words` (e.g., `lease_term_years_words`)
- **Mathematical calculations:** `[base_name]_math` (e.g., `commission_math`)
- **List formatting:** `[base_name]_list` or `[base_name]_comma_list`

#### **Conditional Variables:**
- **Template text variations:** `[concept]_short_form[1,2,3]` for different template contexts
- **Conditional statements:** `[concept]_statement` (e.g., `curfew_statement`)

### **B. VARIABLE PROCESSING STRUCTURE (initialize_all_var.yml)**

```yaml
---
mandatory: True
code: |
 if not defined('user_approves'):
   
   # 1. COLLECT ALL BASIC INPUTS
   need([basic_variable_1])
   need([basic_variable_2])
   [basic_variable_2] = int([basic_variable_2])  # Type conversion as needed
   
   # 2. PROCESS CONDITIONAL LOGIC
   if [condition_variable_yn]:
     need([conditional_variable])
     [derived_variable] = [calculation_function]([conditional_variable])
   else:
     [conditional_variable] = "N/A"
     [derived_variable] = [default_value]
   
   # 3. CALCULATE DERIVED VALUES
   [calculated_variable] = [base_variable] * [multiplier]
   [formatted_variable] = f"${[calculated_variable]:,.2f}"
   [words_variable] = number_to_words([calculated_variable])
   
   # 4. PROCESS COMPLEX DATA (lists, schedules, etc.)
   [complex_data] = [utility_function]([input_parameters])
   
   # 5. DATE CALCULATIONS
   [end_year] = ([start_date].year + [duration_years])
   [end_month_word] = num_to_month([start_date].month)
   
   # 6. DOCUMENT SELECTION LOGIC
   docs_to_show = [[mandatory_doc_1], [mandatory_doc_2]]
   if [condition_1_yn]:
     docs_to_show.append([optional_doc_1])
   if [condition_2_yn]:
     docs_to_show.append([optional_doc_2])
   
   # 7. COMPLETION FLAG
   need(session_tagging_complete)  # If using session tagging
   all_fields_complete = True
---
```

---

## **📝 QUESTIONS.YML STRUCTURE**

### **Required Pattern:**
```yaml
---
question: [Project Name] Information
fields:
 - [Question Label]: [variable_name]
   datatype: [text|number|date|email|yesno|yesnoradio|area|file]
   help: |
     [Optional help text]
 - [Conditional Question]: [conditional_variable]
   datatype: [type]
   show if: [parent_variable_yn]
   help: |
     [Conditional help text]
 - [List Input]: [list_variable]
   datatype: area
   help: |
     [Instructions for multi-line input, format example]
 - [File Upload]: [file_variable]
   datatype: file
   required: false
   accept: |
     "image/jpeg, image/png"
   help: |
     [File upload instructions]
---
```

### **Key Field Datatype Standards:**
- **Text inputs:** `datatype: text`
- **Numbers:** `datatype: number`
- **Currency:** `datatype: number` (format in initialize_all_var.yml)
- **Dates:** `datatype: date`
- **Yes/No decisions:** `datatype: yesnoradio`
- **Multi-line text:** `datatype: area`
- **File uploads:** `datatype: file`

---

## **📧 EMAIL TEMPLATE ARCHITECTURE**

### **A. EMAIL_FUNCTION.YML STRUCTURE**

```yaml
---
modules:
  - docassemble.base.util
---
code: |
  import os
  
  # 1. DOCUMENT LIST FORMATTING FUNCTION
  def format_document_list(docs):
    doc_names = []
    for doc in docs:
        if hasattr(doc, 'info'):
            doc_names.append(doc.info.get('name', 'Document'))
        elif hasattr(doc, 'filename'):
            doc_names.append(os.path.splitext(doc.filename)[0])
        else:
            doc_names.append('Document')
    return doc_names

  attachment_list = format_document_list(docs_to_show)

  # 2. LIST PROCESSING FUNCTIONS (as needed)
  def get_[entity]_list([input_text]):
    if not [input_text]:
        return []
    return [name.strip() for name in [input_text].split('\n') if name.strip()]

  individual_[entities] = get_[entity]_list([entity_variable])
  [entity]_comma_list = ', '.join(individual_[entities]) if individual_[entities] else 'None'
---

template: email_template
subject: |
  [Document Type] for ${[key_identifier_1]}, ${[key_identifier_2]}
content: |
  <strong><u>Date:</u></strong> ${today()}
  
  <strong><u>[SECTION 1 NAME]:</u></strong>
  <ul>
    <li>[Field Label]: ${[variable_name]}</li>
    <li>[Field Label]: ${[variable_name]}</li>
  </ul>
  
  <strong><u>[SECTION 2 NAME]:</u></strong>
  <ul>
    <li>[Field Label]: ${[variable_name]}</li>
    <li>[Conditional Field]: ${[variable_name] if [condition_yn] else "N/A"}</li>
  </ul>
  
  <strong><u>[COMPLEX DATA SECTION]:</u></strong>
  <ul>
    % for line in [html_formatted_data].split('<br>'):
      % if line.strip():
        <li>${line}</li>
      % endif
    % endfor
  </ul>
  
  <strong><u>ATTACHED FILES:</u></strong>
  <ul>
    % for name in attachment_list: 
      <li>${name}</li>
    % endfor
  </ul>

  % if individual_[entities]:
    % for i, [entity] in enumerate(individual_[entities]):
  <strong><u>[ENTITY] CHECKLIST - ${[entity].upper()}:</u></strong>
  <form>
    <div style="margin-left: 20px;">
      <input type="checkbox" id="[item1]_${i}"> <label for="[item1]_${i}">[Checklist Item 1]</label><br>
      <input type="checkbox" id="[item2]_${i}"> <label for="[item2]_${i}">[Checklist Item 2]</label><br>
    </div>
  </form>
  <br>
    % endfor
  % endif

  <strong><u>[MAIN] CHECKLIST:</u></strong>
  <form>
    <div style="margin-left: 20px;">
      <input type="checkbox" id="[item1]"> <label for="[item1]">[Main Checklist Item 1]</label><br>
      <input type="checkbox" id="[item2]"> <label for="[item2]">[Main Checklist Item 2]</label><br>
      % if [conditional_boolean]:
      <input type="checkbox" id="[conditional_item]"> <label for="[conditional_item]">[Conditional Item]</label><br>
      % endif
    </div>
  </form>  
  
  Please retain this email for your records. These values can be used to recreate the documents if needed.
---

question: |
  Where should we send the documents?
fields:
  - Email: recipient_email
    datatype: email
---

question: |
  Documents Sent Successfully
subquestion: |
  Your documents have been sent to ${recipient_email}.
  All generated documents were included in the email.
event: email_sent
---

question: |
  Error Sending Documents
subquestion: |
  There was an error sending your documents to ${recipient_email}.
  Please try again or contact support if the problem persists.
event: email_error
```

---

## **📄 DOCUMENT ATTACHMENT PATTERNS**

### **A. PRIMARY ATTACHMENT FILE (attaching_mandatory_docx.yml)**

```yaml
---
mandatory: True
question: |
 Here is your document.
allow emailing: True
email template: email_template
attachment code: |
 docs_to_show
---

attachment:
 name: [Primary Document Name]
 filename: [Primary Document Name]
 docx template file: [template_file_name].docx
 valid formats:
   - pdf
   - docx
 variable name: [primary_document_variable]
 
---

attachment:
 name: [Secondary Document Name]
 filename: [Secondary Document Name]
 docx template file: [secondary_template].docx
 valid formats:
   - pdf
   - docx
 variable name: [secondary_document_variable]
---
```

### **B. INDIVIDUAL ATTACHMENT FILES (attach_[type].yml)**

```yaml
---
attachment:
 name: [Specific Document Name]
 filename: [Specific Document Name]
 docx template file: [specific_template].docx
 valid formats:
   - pdf
   - docx
 variable name: [specific_doc_variable]
---
```

---

## **🛠️ UTILITY FUNCTION PATTERNS**

### **A. FORMATTING FUNCTIONS**

#### **List Formatting (format_comma_list.yml):**
```yaml
---
code: |
  def format_comma_list(text):
    if not text:
      return ""
    items = [item.strip() for item in text.split('\n') if item.strip()]
    if len(items) == 0:
      return ""
    elif len(items) == 1:
      return items[0]
    elif len(items) == 2:
      return f"{items[0]} and {items[1]}"
    else:
      return ", ".join(items[:-1]) + ", and " + items[-1]

  def format_[entity]_list(text):
    if not text:
      return ""
    names = [name.strip() for name in text.split('\n') if name.strip()]
    return "\n".join(f"• {name}" for name in names)
---
```

#### **Number Conversion (number_to_words.yml):**
```yaml
---
code: |
  def number_to_words(n):
    from num2words import num2words
    words = num2words(n)
    words = words.replace(' ', '\u00A0')  # Non-breaking spaces for Word
    return words
---
```

#### **Date/Time Utilities (num_to_month.yml):**
```yaml
---
code: |
  def num_to_month(num):
    months = {
      1: "January", 2: "February", 3: "March",
      4: "April", 5: "May", 6: "June",
      7: "July", 8: "August", 9: "September",
      10: "October", 11: "November", 12: "December"
    }
    return months.get(num, "Invalid month")
---
```

### **B. COMPLEX CALCULATION FUNCTIONS**

#### **Schedule/Table Generation Pattern:**
```yaml
---
code: |
  def create_[data_type]_schedule([parameters]):
    [data_structure] = []
    
    if [condition_type] == "[type_1]":
      # Calculation logic for type 1
      for [iterator] in range([range_params]):
        [calculated_value] = [calculation_function]([params])
        [data_structure].append([format_function]([iterator], [calculated_value]))
    else:  # alternative type
      # Alternative calculation logic
      [parsed_input] = [input_processing_function]([input_parameter])
      for [iterator] in range([range_params]):
        [calculated_value] = [alternative_calculation]([params])
        [data_structure].append([format_function]([iterator], [calculated_value]))
    
    return [formatted_output]
  
  def generate_[data_type]_html([parameters]):
    # HTML version for email templates
    [html_data] = []
    [same_logic_as_above_but_html_formatted]
    return "<br>".join([html_data])
---
```

---

## **📊 SUMMARY GENERATION PATTERN**

### **summary.yml Structure:**
```yaml
---
code: |
  from docassemble.base.util import DAFile

  # Step 1: Create a DAFile object
  interview_summary = DAFile()
  interview_summary.initialize(filename="interview_summary.txt")

  # Step 2: Retrieve all interview variables dynamically
  interview_vars = dict(globals())

  # Step 3: Filter out system variables
  exclude_vars = ["interview_summary", "__builtins__", "__name__", "__doc__", "__package__", "__loader__", "__spec__"]
  filtered_vars = {k: v for k, v in interview_vars.items() if k not in exclude_vars and not k.startswith("_")}

  # Step 4: Format data and ensure it's not empty
  if filtered_vars:
      summary_content = "\n".join([f"{var}: {value}" for var, value in filtered_vars.items()])
  else:
      summary_content = "No responses recorded."

  # Step 5: Write to the text file
  interview_summary.write(summary_content)
  interview_summary.commit()
---
```

---

## **✅ IMPLEMENTATION CHECKLIST**

### **Before Starting Any New Project:**

#### **Phase 1: Planning**
- [ ] Identify all document types to be generated
- [ ] Map out all required data inputs
- [ ] Design variable naming convention following established patterns
- [ ] Plan conditional logic and document inclusion rules
- [ ] Design email template sections and checklists

#### **Phase 2: Core Structure**
- [ ] Create main interview file with proper includes
- [ ] Set up config.yml with project metadata
- [ ] Implement authentication.yml (copy pattern exactly)
- [ ] Set up modules.yml with required dependencies
- [ ] Create questions.yml with all user inputs

#### **Phase 3: Processing Logic**
- [ ] Build initialize_all_var.yml following the 7-step pattern
- [ ] Create all necessary utility functions
- [ ] Implement complex calculation functions
- [ ] Set up conditional logic for document inclusion

#### **Phase 4: Templates & Output**
- [ ] Create Word document templates with proper variable names
- [ ] Set up attachment files for each document type
- [ ] Build email template with proper sections
- [ ] Implement summary generation

#### **Phase 5: Testing**
- [ ] Test all conditional paths
- [ ] Verify email template formatting
- [ ] Test document generation with various input combinations
- [ ] Validate variable calculations and derived values

---

## **🚨 CRITICAL SUCCESS FACTORS**

### **DO's:**
1. **ALWAYS** follow the established naming conventions
2. **ALWAYS** use the 7-step initialize_all_var.yml pattern
3. **ALWAYS** implement proper conditional logic for optional documents
4. **ALWAYS** create both text and HTML versions of complex data for templates
5. **ALWAYS** include comprehensive email templates with checklists
6. **ALWAYS** use utility functions for formatting and calculations
7. **ALWAYS** implement authentication if required

### **DON'Ts:**
1. **NEVER** create variables that don't follow naming patterns
2. **NEVER** skip the central variable processing in initialize_all_var.yml
3. **NEVER** hardcode calculations in templates - use derived variables
4. **NEVER** forget to handle conditional document inclusion
5. **NEVER** omit error handling in email send functions
6. **NEVER** create redundant variables - use established ones
7. **NEVER** skip the summary generation functionality

---

## **🎯 FINAL IMPLEMENTATION NOTES**

This architecture pattern has proven highly successful for complex document generation interviews. The key to success is:

1. **Consistency** - Follow patterns exactly
2. **Modularity** - Keep functions and logic separated
3. **Scalability** - Use the established variable patterns to enable easy template additions
4. **User Experience** - Rich email templates and comprehensive checklists
5. **Maintainability** - Clear file organization and commenting

**When implementing any new DocAssemble project following this pattern, start with this directive and adapt the specific variable names, document types, and business logic while maintaining the exact same architectural structure.**

---

*This directive is based on analysis of a production-ready, highly successful DocAssemble lease agreement generation system and should be used as the foundation for all similar projects.*