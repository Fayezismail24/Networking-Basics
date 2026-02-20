## Question

Which are a necessary section in `/queue simple` to set bandwidth limitation?

* Target-address, max-limit, dst-address
* Max-limit
* Target-address, dst-address
* Target-address, max limit

## Answer

**Target-address, max limit**

## Explanation

In the `/queue simple` section:

* The `target-address` parameter is necessary to specify the IP address or address range to which the bandwidth limitation will be applied.
* The `max-limit` parameter is necessary to define the maximum allowed bandwidth for the specified target address.

Therefore, the correct answer is **target-address, max limit**.

The other options either:

* Do not include both required parameters, or
* Include unnecessary parameters such as `dst-address`.
