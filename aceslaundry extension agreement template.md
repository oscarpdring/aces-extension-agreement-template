{{ agreement_type }} Extension & Modification Agreement

This {{ agreement_type }} Extension & Modification Agreement (the "Agreement") is dated as of {{ original_agreement_date }} by and between {{ landlord_entity }} ("{{ landlord_role }}"), and {{ tenant_entity }} ("{{ tenant_role }}"){% if good_guy_guaranty_yn %}, and {{ guarantor_entity }} ("Guarantor"){% endif %}

WHEREAS, {{ landlord_role }} and {{ tenant_role }} entered into a certain Laundry Room {{ agreement_type }} (the "{{ agreement_type }}") for certain laundry room premises located at {{ premises_address }} and more particularly described in the {{ agreement_type }} (the "Premises"); and

{% if good_guy_guaranty_yn %}
WHEREAS, each Guarantor entered into a certain Good Guy Guaranty of the {{ agreement_type }} (the "Guaranty"); and
{% endif %}

WHEREAS, {{ landlord_role }} and {{ tenant_role }} have agreed to modify the {{ agreement_type }} upon the terms and conditions hereinafter set forth; and

NOW, THEREFORE, in consideration of ten dollars ($10) and other good and valuable consideration, the receipt and sufficiency of which is hereby acknowledged, the parties hereto agree as follows: 
1.  Basic Terms and Conditions:

{% if extending_term_yn %}
1.1 Extension of term:
The {{ agreement_type_lower }} is hereby extended such that it shall now expire on {{ extension_expiration_date }}.

1.2 Term:
The term of this {{ agreement_type_lower }} shall be the period commencing on the commencement date and ending on the {{ extension_expiration_date }}.
{% else %}
1.1 Extension of term: INTENTIONALLY OMITTED

1.2 Term: INTENTIONALLY OMITTED
{% endif %}

{% if modifying_equipment_yn %}
1.3 Equipment Upgrades and Removals:
{% if equipment_removal_yn %}
{{ tenant_role }} shall remove {{ equipment_removal_details }}
{% endif %}
{% if equipment_installation_yn %}
{{ tenant_role }} shall install {{ equipment_installation_details }} 
{% endif %}
{% if equipment_upgrade_yn %}
{{ tenant_role }} shall upgrade on-site {{ equipment_upgrade_details }}
{% endif %}
{% else %}
1.3 Equipment Upgrades and Removals: INTENTIONALLY OMITTED
{% endif %}

{% if modifying_rent_yn %}
1.4 Rent shall be amended such that:
{{ tenant_role }} shall pay to {{ landlord_role }} Rent calculated as percentage rental, in a sum equal to the amount, calculated as the Applicable Percentage of Gross Sales greater than the Gross Sales Breakpoint, as herein defined, at the Premises in each calendar month. {{ tenant_role }} shall submit to {{ landlord_role }} on or before {{ reporting_days_after_month_words }} ({{ reporting_days_after_month }}) days following the completion of each month a written statement showing in reasonable detail the amount of Gross Receipts for the preceding calendar month. Such monthly statements shall be accompanied by a payment of the percentage rental, if any, due for the preceding calendar month. The term "Gross Sales," as used in this {{ agreement_type }} shall mean the amount of sales of all merchandise and services sold or rendered, in, about or from the Premises by the {{ tenant_role }} minus refunds, vandalism related expenses, internet fees, and credit card processing fees, whether for cash or credit including but not limited to, such sales and services: (a) where orders originate at or are accepted by {{ tenant_role }} at the Premises, but delivery thereof is made from or at a place other than the Premises or (b) by means of vending machines in the Premises. The term "Applicable Percentage," as used in this {{ agreement_type }} extension and modification agreement, shall mean {{ applicable_percentage_amount }}%. The term "Gross Sales Breakpoint," as used in this {{ agreement_type }} extension and modification agreement, shall mean {{ gross_sales_breakpoint_amount_decimal }}.
{% else %}
1.4 Rent Modification: INTENTIONALLY OMITTED
{% endif %}

{% if rent_schedule_yn %}
A.   {{ tenant_role }} shall pay {{ landlord_role }} Fixed Rent (sometimes hereinafter also referred to as "Fixed Annual Rent" or "fixed annual rent" or "fixed rent") at the following rates and intervals in advance for each {{ agreement_type }} Year in the Term:
{{ rent_schedule_formatted }}

B.  The term "{{ agreement_type }} Year" shall mean the twelve months commencing on the first day of the month in which occurs the Commencement Date, and each subsequent period of twelve months.
{% endif %}

{% if modifying_minimum_compensation_yn %}
1.6  Minimum Compensation:
The following text is added to the {{ agreement_type_lower }} agreement:
Notwithstanding any other provision of this {{ agreement_type_lower }} {{ tenant_role }} shall always be entitled to retain a minimum daily compensation for each day of the Term of {{ minimum_compensation_per_machine_per_day_decimal }} per installed machine --- which shall increase by 5% every 12 months from the Commencement Date --- after payment of Rent, refunds, vandalism related expenses, internet fees, and credit card processing fees and, if not, the Rent shall be adjusted accordingly to provide said minimum amount to {{ tenant_role }}.
{% else %}
1.6 Minimum Compensation: INTENTIONALLY OMITTED
{% endif %}

{% if minimum_compensation_increase_yn %}
1.7 Minimum Compensation and Percentage Increase Changes:
Notwithstanding the foregoing, the meter charges for each machine shall increase by {{ percentage_increase_amount_words }} ({{ percentage_increase_amount }}%) on {{ compensation_increase_date }}. For clarification, and in example only, {{ machine_type_example }}, initially metered at {{ original_meter_price_decimal }} per base wash cycle, on {{ compensation_increase_date }}, the metered charge for the base wash cycle shall increase to {{ new_meter_price_decimal }}.
{% else %}
1.7 Minimum Compensation and Percentage Increase Changes: INTENTIONALLY OMITTED
{% endif %}

2.  Miscellaneous:

{% if improvements_yn %}
2.1   Improvements:
{{ tenant_role }} shall {{ work_to_be_done }}
{% else %}
2.1 Improvements: INTENTIONALLY OMITTED
{% endif %}

{% if real_estate_taxes_yn %}
2.2   Real Estate Taxes:
Effective on the Commencement Date, the {{ agreement_type }} is hereby amended in part, such that: (a) the term "Tax Base Factor" shall mean the real estate taxes for the period beginning {{ tax_base_begin_date }} and ending {{ tax_base_end_date }}; (b) the term "comparative year" shall mean the tax year following the year commencing {{ tax_base_begin_date }} and ending {{ tax_base_end_date }}, and each subsequent period of twelve (12) months; and (c) the term "The Percentage," for purposes of computing tax escalation, shall be deemed to mean {{ tax_percentage_amount }}% ({{ tax_percentage_amount_words }}).
{% else %}
2.2 Real Estate Taxes: INTENTIONALLY OMITTED
{% endif %}

2.3    Conflicts
In the event of a conflict between this Agreement and the terms of the {{ agreement_type }} the terms of this Agreement shall control.

2.4    Effect of Modification and Extension
Except as expressly modified by this Agreement, the terms and conditions of the {{ agreement_type }} as modified, are hereby ratified and confirmed and shall continue in full force and effect.

2.5    Execution
This Agreement may be executed by electronic, digital or equivalent signature and it may also be executed in counterparts.

In Witness Whereof, the parties have executed this Agreement as of the date first stated above.

{{ landlord_role }}: {{ landlord_entity }}
By: _________________________

{{ tenant_role }}: {{ tenant_entity }}
By: _________________________     
{% if good_guy_guaranty_yn %}
 
Guarantor: {{ guarantor_entity }}
              By: _________________________
{% endif %}                        


