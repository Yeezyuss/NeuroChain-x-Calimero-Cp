'use client';

import { useEffect, useState } from 'react';
import Image from 'next/image';

export function Preloader() {
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    const timer = setTimeout(() => {
      setLoading(false);
    }, 2500);

    return () => clearTimeout(timer);
  }, []);

  if (!loading) return null;

  return (
    <div className="preloader">
      <div className="neural-network-container">
        <Image
          src="https://i.makeagif.com/media/7-23-2019/q3ItDm.gif"
          alt="Neural Network"
          width={400}
          height={400}
          className="neural-network-gif"
        />
      </div>
      <div className="loading-text">Initializing AI Marketplace</div>
    </div>
  );
}