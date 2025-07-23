# B2L
B2L basketball league

import React from 'react';

interface ResetButtonProps {
  onClick: () => void;
}

const RefreshIcon: React.FC<{className?: string}> = ({ className }) => (
    <svg xmlns="http://www.w3.org/2000/svg" className={className} fill="none" viewBox="0 0 24 24" stroke="currentColor" strokeWidth={2}>
        <path strokeLinecap="round" strokeLinejoin="round" d="M4 4v5h5M20 20v-5h-5M4 4l1.5 1.5A9 9 0 0120.5 10M20 20l-1.5-1.5A9 9 0 003.5 14" />
    </svg>
);

const ResetButton: React.FC<ResetButtonProps> = ({ onClick }) => {
  return (
    <button
      onClick={onClick}
      className="inline-flex items-center gap-2 bg-red-800 hover:bg-red-700 text-white font-semibold py-2 px-6 rounded-full transition-all duration-200 ease-in-out transform hover:scale-105 active:scale-100 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-offset-gray-900 focus:ring-red-500"
    >
      <RefreshIcon className="h-5 w-5" />
      スコアリセット
    </button>
  );
};

export default ResetButton;
