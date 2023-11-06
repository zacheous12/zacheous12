import subprocess

def get_wifi_password():
    """
    Function to retrieve the password of the currently connected WiFi network.

    Returns:
    - str:
        The password of the currently connected WiFi network.

    Raises:
    - OSError:
        If the command to retrieve the WiFi password fails.
    """

    try:
        # Run the command to retrieve the WiFi password
        output = subprocess.check_output(["netsh", "wlan", "show", "profile"]).decode("utf-8")

        # Find the name of the currently connected WiFi network
        connected_network = [line.split(":")[1].strip() for line in output.splitlines() if "All User Profile" in line][0]

        # Run the command to retrieve the password of the currently connected WiFi network
        password_output = subprocess.check_output(["netsh", "wlan", "show", "profile", "name=" + connected_network, "key=clear"]).decode("utf-8")

        # Find the password in the output
        password = [line.split(":")[1].strip() for line in password_output.splitlines() if "Key Content" in line][0]

        return password

    except subprocess.CalledProcessError as e:
        raise OSError("Failed to retrieve WiFi password.") from e

# Example usage:
try:
    wifi_password = get_wifi_password()
    print(f"The password of the currently connected WiFi network is: {wifi_password}")
except OSError as e:
    print(f"Error: {e}")
