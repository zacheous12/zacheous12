def calculator():
    """
    Function to perform basic arithmetic calculations based on user input.

    This function prompts the user to enter two numbers and an operator (+, -, *, /).
    It then performs the corresponding arithmetic operation and returns the result.

    Returns:
    - float:
        The result of the arithmetic operation.

    Raises:
    - ValueError:
        If the user enters an invalid operator or if the second number is zero when performing division.
    """

    # Prompting the user to enter the first number
    num1 = float(input("Enter the first number: "))

    # Prompting the user to enter the operator
    operator = input("Enter the operator (+, -, *, /): ")

    # Prompting the user to enter the second number
    num2 = float(input("Enter the second number: "))

    # Performing the arithmetic operation based on the operator
    if operator == "+":
        result = num1 + num2
    elif operator == "-":
        result = num1 - num2
    elif operator == "*":
        result = num1 * num2
    elif operator == "/":
        if num2 == 0:
            raise ValueError("Cannot divide by zero.")
        result = num1 / num2
    else:
        raise ValueError("Invalid operator.")

    return result

# Example usage of the calculator function
try:
    result = calculator()
    print("Result:", result)
except ValueError as e:
    print("Error:", e)
