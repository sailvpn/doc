# What is SailX

**SailX** is an anonymous, prepaid VPN service.

# How SailX Works

SailX can be configured to operate in two distinct modes: **Anonymous Mode** and **Registered Mode**. Users can switch between these modes at any time, but each mode requires a different type of token.

## 1. Anonymous Mode

### Client Configuration

- **Desktop:** Set `params.crypto=JWT2`
- **Android Apps:** Set **Authentication Method** to `JWT2`

### How it Works

In Anonymous Mode, you do not need to create an account. Instead, you purchase a **JWT RSA token** that contains a one-time random ID and a specific data quota. You load this token directly into your VPN client to start using the service. The serving VPN proxy node has absolutely zero knowledge of your identity.

### Purchase & Setup Process

1.  **Select a Package:** Visit [SailX Packages](https://sailsecuretech.com) or [SailX Offers](https://sailsecuretech.com/offer) to view available packages and pricing.
2.  **Payment:** Click **Buy Anonymous Pass** to be redirected to the secure Stripe checkout page to enter your card or wallet information.
3.  **Token Retrieval:** After a successful payment, you will be redirected to [SailX Stripe Confirmation](https://sailsecuretech.com/stripe), where your unique JWT RSA token will be generated.

> ⚠️ **IMPORTANT:** The token is generated and displayed **ONLY ONCE**. If you do not save or copy it, it is lost forever. The system does not store your tokens.

4.  **Installation:** Download the client software package from [SailX Downloads](https://sailsecuretech.com/download). Unzip or install the package.
5.  **Configuration:** Configure the client using your saved token and the VPN proxy node details found at [SailX Nodes](https://sailsecuretech.com/nodes).

_For detailed instructions and technical guides, refer to the `README` file inside the downloaded package, visit [SailX Documentation](https://sailsecuretech.com/docs), or contact support at [SailX Support](https://sailsecuretech.com/support)._

### Checking Balance

You can verify your token's remaining data balance at any time by entering or uploading your token at [SailX Token Checker](https://sailsecuretech.com/check-token) and clicking **Check**.

---

## 2. Registered Mode

### Client Configuration

- **Desktop:** Set `params.crypto=JWT`
- **Android Apps:** Set **Authentication Method** to `JWT`

### How it Works

In Registered Mode, you create and log into an account with the VPN service. Purchased data packages are added directly to your profile balance. You then generate a **JWT SHA256 token**, which contains a temporary random ID linked to your account and an expiration date, and load it into your client.

### Purchase & Setup Process

1.  **Refill Balance:** Go to [SailX Refill](https://sailsecuretech.com/refill) to view available packages and prices.
2.  **Payment:** Click **Add to Profile Balance** for your chosen package to proceed to Stripe checkout.
3.  **Confirmation:** Once payment is complete, you will be redirected back to [SailX Stripe Confirmation](https://sailsecuretech.com/stripe). The platform automatically detects your registered status, displays a success message, and adds the data quota to your account profile.
4.  **Token Generation:** Visit [SailX Token Generation](https://sailsecuretech.com/token) to generate your custom JWT SHA256 token.
5.  **Configuration:** Follow the same installation and configuration steps used in Anonymous Mode to set up your client.

---

# Prepaid Data Features

- **No Expiration:** In both modes, data is purchased as a one-time prepaid package. Your data never expires and remains active as long as you maintain a positive balance.

---

# Privacy & Anonymity

Your payment information and your VPN usage are **deliberately decoupled**.

- The VPN system does not store any records of your credit cards or purchasing activities.
- It is technically impossible to establish a 1-to-1 link between a user's payment method/billing history and a JWT RSA token or registered VPN account.
