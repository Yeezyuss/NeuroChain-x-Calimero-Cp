'use client';

import { useCallback, useEffect, useState } from 'react';
import { AuthClient } from '@dfinity/auth-client';
import { Button } from './ui/button';
import { Wallet } from 'lucide-react';

export function ICPConnectButton() {
  const [authClient, setAuthClient] = useState<AuthClient | null>(null);
  const [isAuthenticated, setIsAuthenticated] = useState(false);

  useEffect(() => {
    AuthClient.create().then(client => {
      setAuthClient(client);
      const isAuth = client.isAuthenticated();
      setIsAuthenticated(isAuth);
    });
  }, []);

  const login = useCallback(async () => {
    if (!authClient) return;

    const days = BigInt(1);
    const hours = BigInt(24);
    const nanoseconds = BigInt(3600000000000);

    await authClient.login({
      identityProvider: process.env.NEXT_PUBLIC_II_URL || 'https://identity.ic0.app',
      maxTimeToLive: days * hours * nanoseconds,
      onSuccess: () => {
        setIsAuthenticated(true);
      },
    });
  }, [authClient]);

  const logout = useCallback(async () => {
    if (!authClient) return;
    await authClient.logout();
    setIsAuthenticated(false);
  }, [authClient]);

  return (
    <Button
      onClick={isAuthenticated ? logout : login}
      variant={isAuthenticated ? "outline" : "default"}
    >
      <Wallet className="w-4 h-4 mr-2" />
      {isAuthenticated ? 'Disconnect' : 'Connect ICP'}
    </Button>
  );
}