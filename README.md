# encapsulation
class Staff:
    def init(self, s_name: str, access_code: str):
        """
        Initializes a Staff member.
        s_name is Public, __access_code is Private.
        """
        self.s_name = s_name
        # Set the private attribute through the property setter to enforce length validation right away
        self.access_code = access_code

    @property
    def access_code(self) -> str:
        """
        Getter property: Allows authorized view of the access code.
        """
        # In a real system, you might prompt for authentication here.
        return self.__access_code

    @access_code.setter
    def access_code(self, new_code: str):
        """
        Setter property: Updates the access code after validating its length.
        Requires the access code to be between 4 and 8 characters long.
        """
        if 4 <= len(new_code) <= 8:
            self.__access_code = new_code
        else:
            print(f"Error: Access code '{new_code}' must be between 4 and 8 characters long!")

    def display_staff_info(self):
        """
        Displays public and private staff information safely.
        """
        print("\n--- UMaT Staff Access Record ---")
        print(f"Staff Name  : {self.s_name}")
        print(f"Access Code : {self.access_code}")  # Uses the getter property safely
        print("---------------------------------")


# --- Demonstration of the System ---
if name == "main":
    print("1. Creating staff member with a valid code...")
    staff_member = Staff("Dr. Matthew Cobbinah", "UMaT2026")
    staff_member.display_staff_info()

    print("\n2. Attempting to assign an INVALID code (too short)...")
    staff_member.access_code = "123"  # Will trigger validation error
    
    print("\n3. Attempting to assign a VALID new code...")
    staff_member.access_code = "Pass99!"  # Valid length (7 chars)
    staff_member.display_staff_info()

    print("\n4. Proving Name Mangling is active...")
    try:
        # Trying to access the private attribute directly without the property or mangled name
        print(staff_member.__access_code)
    except AttributeError as e:
        print(f"Caught expected error: {e}")
