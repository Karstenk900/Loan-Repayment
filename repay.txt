
# ============================================
# LOAN PAYMENT CALCULATOR WEB APP
# Built using Python and Streamlit
# ============================================

# 1. Import Streamlit
import streamlit as st


# 2. Configure the webpage
st.set_page_config(
    page_title="Loan Payment Calculator",
    page_icon="💰",
    layout="centered"
)


# 3. Create the webpage title and introduction
st.title("💰 Loan Payment Calculator")

st.write(
    "Welcome to the Loan Payment Calculator! "
    "Enter your loan information below to calculate "
    "your estimated monthly payment."
)

st.divider()


# 4. Create an input box for the loan amount
loan_amount = st.number_input(
    "Enter Loan Amount ($):",
    min_value=0.01,
    value=25000.00,
    step=1000.00,
    format="%.2f"
)


# 5. Create an input box for the annual interest rate
interest_rate = st.number_input(
    "Enter Annual Interest Rate (%):",
    min_value=0.0,
    value=5.0,
    step=0.25,
    format="%.2f"
)


# 6. Create an input box for the loan term
loan_term = st.number_input(
    "Enter Loan Term (Years):",
    min_value=1,
    value=5,
    step=1
)


# 7. Create the Calculate button
if st.button("Calculate Loan Payment", use_container_width=True):

    # Convert annual interest rate to a monthly rate
    monthly_interest_rate = interest_rate / 100 / 12

    # Convert loan years into total monthly payments
    number_of_payments = loan_term * 12

    # 8. Calculate the monthly loan payment

    if monthly_interest_rate == 0:

        # Formula when there is no interest
        monthly_payment = loan_amount / number_of_payments

    else:

        # Standard loan payment formula
        monthly_payment = (
            loan_amount * monthly_interest_rate *
            (1 + monthly_interest_rate) ** number_of_payments
        ) / (
            (1 + monthly_interest_rate) ** number_of_payments - 1
        )

    # 9. Calculate total repayment and total interest

    total_payment = monthly_payment * number_of_payments

    total_interest = total_payment - loan_amount

    # 10. Display a success message
    st.success("Loan payment calculated successfully!")

    # 11. Display the monthly payment
    st.subheader("Loan Payment Results")

    st.metric(
        label="Estimated Monthly Payment",
        value=f"${monthly_payment:,.2f}"
    )

    # 12. Display additional loan information

    col1, col2 = st.columns(2)

    with col1:
        st.metric(
            label="Total Interest",
            value=f"${total_interest:,.2f}"
        )

    with col2:
        st.metric(
            label="Total Repayment",
            value=f"${total_payment:,.2f}"
        )

    # 13. Display the loan details

    st.subheader("Loan Details")

    st.write(f"Loan Amount: ${loan_amount:,.2f}")

    st.write(f"Annual Interest Rate: {interest_rate:.2f}%")

    st.write(f"Loan Term: {loan_term} years")

    st.write(f"Number of Monthly Payments: {number_of_payments}")

    # 14. Display the mathematical formula

    st.subheader("Formula Used")

    if interest_rate == 0:

        formula = "Monthly Payment = Loan Amount / Number of Payments"

    else:

        formula = "M = P × [r(1 + r)^n] / [(1 + r)^n - 1]"

    st.code(formula, language="text")

    # 15. Explain the formula variables

    st.write("Where:")

    st.write("M = Monthly loan payment")

    st.write("P = Original loan amount")

    st.write("r = Monthly interest rate")

    st.write("n = Total number of monthly payments")


# 16. Add information at the bottom of the webpage

st.divider()

st.subheader("About This App")

st.write(
    "This application calculates estimated monthly loan "
    "payments based on the loan amount, annual interest "
    "rate, and loan repayment term."
)

st.caption(
    "Loan Payment Calculator | Built with Python and Streamlit"
)
