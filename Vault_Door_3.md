# SOLVE
source file:
```bash
class VaultDoor3 {
    public static void main(String args[]) {
        VaultDoor3 vaultDoor = new VaultDoor3();
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter vault password: ");
        String userInput = scanner.next();
	String input = userInput.substring("picoCTF{".length(),userInput.length()-1);
	if (vaultDoor.checkPassword(input)) {
	    System.out.println("Access granted.");
	} else {
	    System.out.println("Access denied!");
        }
    }

    // Our security monitoring team has noticed some intrusions on some of the
    // less secure doors. Dr. Evil has asked me specifically to build a stronger
    // vault door to protect his Doomsday plans. I just *know* this door will
    // keep all of those nosy agents out of our business. Mwa ha!
    //
    // -Minion #2671
    public boolean checkPassword(String password) {
        if (password.length() != 32) {
            return false;
        }
        char[] buffer = new char[32];
        int i;
        for (i=0; i<8; i++) {
            buffer[i] = password.charAt(i);
        }
        for (; i<16; i++) {
            buffer[i] = password.charAt(23-i);
        }
        for (; i<32; i+=2) {
            buffer[i] = password.charAt(46-i);
        }
        for (i=31; i>=17; i-=2) {
            buffer[i] = password.charAt(i);
        }
        String s = new String(buffer);
        return s.equals("jU5t_a_sna_3lpm11g54e_u_4_m4r042");
    }
}
```
we have been given the scrambled password, to unscramble it write a py script or do manually
final script:
```bash
target = "jU5t_a_sna_3lpm11g54e_u_4_m4r042"
password = [''] * 32

# Step 1 reverse
for i in range(8):
    password[i] = target[i]

# Step 2 reverse
for i in range(8,16):
    password[23-i] = target[i]

# Step 3 reverse
for i in range(16,32,2):
    password[46-i] = target[i]

# Step 4 reverse
for i in range(31,16,-2):
    password[i] = target[i]

print("".join(password))
```
## FLAG
picoCTF{jU5t_a_s1mpl3_an4gr4m_4_u_e45012}
