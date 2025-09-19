import React, { useState } from 'react';
import RaffleHeader from '@/components/RaffleHeader';
import RaffleGrid from '@/components/RaffleGrid';
import RaffleSummary from '@/components/RaffleSummary';
import { toast } from '@/hooks/use-toast';

const Index = () => {
  const [selectedNumbers, setSelectedNumbers] = useState<number[]>([]);

  const handleNumberSelect = (number: number) => {
    setSelectedNumbers(prev => [...prev, number]);
  };

  const handleClearSelection = () => {
    setSelectedNumbers([]);
    toast({
      title: "Seleção limpa",
      description: "Todos os números foram desmarcados.",
    });
  };

  const handleProceedToPayment = () => {
    toast({
      title: "Redirecionando para pagamento",
      description: `Total: R$ ${(selectedNumbers.length * 15).toFixed(2)}`,
    });
  };

  return (
    <div className="min-h-screen bg-gradient-to-br from-rose-50 via-rose-25 to-white">
      <div className="container mx-auto px-4 py-8 max-w-7xl">
        
        {/* Header da Rifa */}
        <RaffleHeader />
        
        {/* Layout Principal */}
        <div className="grid grid-cols-1 lg:grid-cols-3 gap-8">
          
          {/* Grid de Números */}
          <div className="lg:col-span-2">
            <RaffleGrid 
              selectedNumbers={selectedNumbers}
              onNumberSelect={handleNumberSelect}
            />
          </div>
          
          {/* Resumo da Compra */}
          <div className="lg:col-span-1">
            <div className="sticky top-8">
              <RaffleSummary 
                selectedNumbers={selectedNumbers}
                onClearSelection={handleClearSelection}
                onProceedToPayment={handleProceedToPayment}
              />
            </div>
          </div>
        </div>

        {/* Footer */}
        <div className="mt-12 text-center">
          <p className="text-rose-500 text-sm">
            🌹 Boa sorte! Que a sorte esteja ao seu lado! 🌹
          </p>
        </div>
      </div>
    </div>
  );
};

export default Index;
