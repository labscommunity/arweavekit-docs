---
description: The Connect Button provides an option to easily integrate the Wallet Kit
---

# Connect Button

The `<ConnectButton>` component is a highly customizable button that supports the [ANS](https://ans.gg) protocol to display information about the connected wallet. It comes as part of the `@arweave-wallet-kit/react` package.

## Usage

You can import and use the component anywhere in your React application as follows:

```tsx
<ConnectButton
  accent="rgb(255, 0, 0)"
  profileModal={false}
  showBalance={true}
  ...
/>
```

## Configuration

You can configure the Connect Button through its props:

| Props                | Type      | Description                                                                             |
| -------------------- | --------- | --------------------------------------------------------------------------------------- |
| `accent`             | `string`  | A theme color for the button                                                            |
| `showBalance`        | `boolean` | Show user balance when connected                                                        |
| `showProfilePicture` | `boolean` | Show user profile picture when connected                                                |
| `useAns`             | `boolean` | Use ANS to grab profile information                                                     |
| `profileModal`       | `boolean` | Show profile modal on click (if disabled, clicking the button will disconnect the user) |

