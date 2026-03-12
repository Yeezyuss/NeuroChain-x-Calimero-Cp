'use client';

import { DynamicContextProvider, DynamicWidget as DynamicWidgetCore } from '@dynamic-labs/sdk-react-core';

const settings = {
  environmentId: process.env.NEXT_PUBLIC_DYNAMIC_ENVIRONMENT_ID!,
  walletConnectors: [
    'metamask',
    'phantom',
    'keplr',
    'coinbase',
    'walletconnect',
    'brave',
    'rainbow'
  ],
  walletConnectorOptions: {
    showQrModal: true,
    showAllWallets: true,
  },
  evmNetworks: [
    { chainId: 1, name: 'Ethereum' },
    { chainId: 137, name: 'Polygon' },
    { chainId: 56, name: 'BNB Chain' }
  ],
  settings: {
    walletList: {
      displayAllWallets: true,
      searchable: true
    }
  }
};

export function DynamicWidget() {
  return (
    <DynamicContextProvider settings={settings}>
      <DynamicWidgetCore
        innerButtonComponent={<span>Connect Wallet</span>}
        variant="modal"
      />
    </DynamicContextProvider>
  );
}