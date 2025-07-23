# B2L
B2L basketball league


import React, { useState, useEffect } from 'react';

interface PlayerSelectionModalProps {
  isOpen: boolean;
  team: 'home' | 'away';
  points: number;
  onSelect: (playerNumber: number) => void;
  onMiss: (playerNumber: number) => void;
  onClose: () => void;
}

const PLAYER_NUMBERS = [4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 99];

const PlayerSelectionModal: React.FC<PlayerSelectionModalProps> = ({ isOpen, team, points, onSelect, onMiss, onClose }) => {
  const [isMiss, setIsMiss] = useState(false);

  useEffect(() => {
    if (isOpen) {
      setIsMiss(false); // Reset state when modal opens
    }
  }, [isOpen]);

  if (!isOpen) return null;

  const teamName = team === 'home' ? 'HOME' : 'AWAY';
  const teamColorClass = team === 'home' ? 'text-cyan-400' : 'text-rose-400';
  const borderColor = team === 'home' ? 'border-cyan-500' : 'border-rose-500';
  const buttonHoverColor = team === 'home' ? 'hover:bg-cyan-500' : 'hover:bg-rose-500';

  const handleMissButtonClick = () => {
    setIsMiss(true);
  };

  const handlePlayerClick = (playerNumber: number) => {
    if (isMiss) {
      onMiss(playerNumber);
    } else {
      onSelect(playerNumber);
    }
  };

  return (
    <div 
        className="fixed inset-0 bg-black/70 backdrop-blur-sm flex items-center justify-center z-50 p-4"
        onClick={onClose}
        aria-modal="true"
        role="dialog"
    >
      <div 
        className={`bg-gray-800 rounded-2xl shadow-2xl w-full max-w-md border-2 ${borderColor} p-6 m-4 animate-fade-in`}
        onClick={(e) => e.stopPropagation()}
      >
        <div className="flex justify-between items-center mb-4">
            <div className="flex items-center gap-4">
                <h2 className="text-2xl font-bold">
                    {isMiss ? (
                        <span className="text-orange-400">MISS</span>
                    ) : (
                        <>
                            <span className={teamColorClass}>{teamName}</span> +{points}P
                        </>
                    )}
                </h2>
                {!isMiss && (
                    <button 
                        onClick={handleMissButtonClick} 
                        className="bg-orange-600 hover:bg-orange-500 text-white font-bold py-1 px-3 rounded-md transition-colors text-sm"
                        aria-label="Mark attempt as miss"
                    >
                        ミス
                    </button>
                )}
            </div>
            <button onClick={onClose} className="text-gray-400 hover:text-white transition-colors" aria-label="閉じる">
                <svg xmlns="http://www.w3.org/2000/svg" className="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path strokeLinecap="round" strokeLinejoin="round" strokeWidth={2} d="M6 18L18 6M6 6l12 12" />
                </svg>
            </button>
        </div>

        <p className="text-center text-gray-300 mb-6">
            {isMiss ? 'ミスした選手の番号を選択してください' : '得点した選手の番号を選択してください'}
        </p>

        <div className="grid grid-cols-4 gap-3">
          {PLAYER_NUMBERS.map((number) => (
            <button
              key={number}
              onClick={() => handlePlayerClick(number)}
              className={`p-4 bg-gray-700 text-white font-bold rounded-lg text-xl transition-all duration-200 ease-in-out transform hover:scale-105 ${buttonHoverColor} focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-offset-gray-800 focus:ring-yellow-400`}
            >
              #{number}
            </button>
          ))}
        </div>
      </div>
      <style>{`
        @keyframes fade-in {
          from { opacity: 0; transform: scale(0.95); }
          to { opacity: 1; transform: scale(1); }
        }
        .animate-fade-in {
          animation: fade-in 0.2s ease-out forwards;
        }
      `}</style>
    </div>
  );
};

export default PlayerSelectionModal;
