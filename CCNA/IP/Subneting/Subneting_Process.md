## Step 1: Determine the Number of Bits to Change
- To find out how many bits need to be changed in the original subnet mask to get the new subnet mask, consider the requirements for the number of subnets or hosts required.  
- Use the formula to calculate the number of bits:
  - For subnets: You need to find how many bits are required to create the needed subnets.
  - For hosts: You need to determine how many bits are left for host addresses after subnetting.

## Step 2: Find the New Subnet Mask
- The new subnet mask is determined by adding the bits for subnetting to the original subnet mask.  
- If you’re subnetting a Class C network, for example:
  - Original subnet mask: `255.255.255.0` (or `/24`)
  - If you need 4 subnets, for instance, you will borrow 2 bits (since `2^2 = 4`).
  - The new subnet mask would be `/26` (or `255.255.255.192`).

## Step 3: Find the Increment (Difference Between Subnets)
- The increment (or subnet size) is the difference between each subnet.
- The increment can be calculated by taking `2^(number of borrowed bits)` and subtracting 2 (for network and broadcast addresses).
- For example, if the new subnet mask is `/26`:
  - The increment is `256 - 192 = 64`.

## Step 4: Find the Number of Usable Hosts
- The number of usable hosts in each subnet is determined by the remaining bits for host addresses.
- Use the formula:
  - `Number of Usable Hosts = (2^(number of host bits)) - 2`.
- For example, if you have a `/26` subnet mask, you have 6 host bits (32 - 26 = 6).
  - The number of usable hosts would be `(2^6) - 2 = 62`.

## Step 5: List All Subnets
- List all the subnets by using the new subnet mask and the increment.
- For example, if the network is `192.168.1.0/24` and the new subnet mask is `/26`:
  - The subnets would be:
    - `192.168.1.0/26`
    - `192.168.1.64/26`
    - `192.168.1.128/26`
    - `192.168.1.192/26`

## Step 6: Configure Your Network
- Finally, configure your network using the subnets you created.
  - Assign IP addresses to hosts within each subnet.
  - Make sure your network devices (routers, switches) are aware of the subnetting.
