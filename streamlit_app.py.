import streamlit as st

def loan_approval_algorithm():
    try:
        # User inputs
        loan_amount = st.number_input("Enter the proposed loan amount:", min_value=0.0, step=100.0)
        loan_term = st.number_input("Enter the proposed loan term (in months):", min_value=1, max_value=3, step=1)
        monthly_income = st.number_input("Enter your monthly income:", min_value=0.0, step=100.0)
        monthly_expenses = st.number_input("Enter your monthly expenses:", min_value=0.0, step=100.0)

        # Income streams
        num_income_streams = st.number_input("Enter the number of income streams:", min_value=1, step=1)
        income_streams = []
        total_income = monthly_income  # Include the initial monthly income

        for i in range(int(num_income_streams)):
            income_name = st.text_input(f"Enter the name of income stream {i + 1}:")
            income_value = st.number_input(f"Enter the monthly value of {income_name}:", min_value=0.0, step=100.0)
            if income_name and income_value:
                income_streams.append((income_name, income_value))
                total_income += income_value

        # Collateral
        num_collateral = st.number_input("Enter the number of collateral items:", min_value=1, step=1)
        collateral_value = 0
        collateral_items = []

        for i in range(int(num_collateral)):
            collateral_type = st.text_input(f"Enter the type of collateral item {i + 1}:")
            collateral_item_value = st.number_input(f"Enter the value of {collateral_type}:", min_value=0.0, step=100.0)
            if collateral_type and collateral_item_value:
                collateral_items.append((collateral_type, collateral_item_value))
                collateral_value += collateral_item_value

        # Constraints
        if loan_term > 3:
            st.error("Error: Loan term cannot exceed 3 months.")
            return
        if collateral_value < 2 * loan_amount:
            st.error("Error: Collateral value must be at least twice the loan amount.")
            return

        monthly_interest_rate = 0.15
        total_interest = loan_amount * monthly_interest_rate * loan_term
        total_repayment = loan_amount + total_interest

        monthly_repayment = total_repayment / loan_term
        if monthly_repayment > 0.3 * total_income:
            st.error("Error: Monthly repayments exceed 30% of total income.")
            return

        weekly_repayment = monthly_repayment / 4  # Assuming a 4 week month
        daily_repayment = weekly_repayment / 5  # Assuming 5 workdays a week
        
        st.success("Loan Application Approved!")
        st.write("Requirements Satisfied:")
        st.write(f"- Loan Amount: ${loan_amount}")
        st.write(f"- Loan Term: {loan_term} months")
        st.write(f"- Monthly Repayment: ${monthly_repayment:.2f}")
        st.write(f"- Weekly Repayment: ${weekly_repayment:.2f}")
        st.write(f"- Daily Repayment: ${daily_repayment:.2f}")

    except Exception as e:
        st.error(f"An unexpected error occurred: {e}")

# Streamlit app title
st.title("Loan Approval Algorithm")
loan_approval_algorithm()
