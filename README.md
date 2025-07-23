# B2L
B2L basketball league


import React from 'react';

interface ScoreboardHeaderProps {
  homeScore: number;
  awayScore: number;
  homeFouls: number;
  awayFouls: number;
  homeTimeouts: number;
  awayTimeouts: number;
  quarter: number;
}

const TimeoutIndicator: React.FC<{ count: number; color: string }> = ({ count, color }) => (
  <div className="flex items-center gap-1.5">
    <span>T.O.</span>
    <div className="flex gap-1">
      {Array.from({ length: 1 }).map((_, i) => (
        <div 
          key={i} 
          className={`w-3 h-3 rounded-full transition-colors duration-300 ${i < count ? color : 'bg-gray-600'}`}
        ></div>
      ))}
    </div>
  </div>
);

const ScoreboardHeader: React.FC<ScoreboardHeaderProps> = ({
  homeScore,
  awayScore,
  homeFouls,
  awayFouls,
  homeTimeouts,
  awayTimeouts,
  quarter,
}) => {
  return (
    <header className="w-full max-w-5xl bg-gray-950/80 backdrop-blur-sm border border-gray-700 rounded-xl p-3 md:p-4 shadow-2xl shadow-black/50">
      <div className="flex justify-between items-center text-white">
        {/* HOME Team */}
        <div className="flex items-center gap-3 md:gap-4 w-1/3">
          <span className="text-xl md:text-2xl font-bold text-cyan-400">HOME</span>
          <span className="text-4xl md:text-5xl font-scoreboard text-white">{String(homeScore).padStart(2, '0')}</span>
        </div>

        {/* Quarter Info */}
        <div className="flex flex-col items-center flex-shrink-0">
          <div className="text-xl md:text-3xl font-bold font-scoreboard text-yellow-300 tracking-wider">
            {quarter > 4 ? `OT${quarter - 4}` : `Q${quarter}`}
          </div>
        </div>

        {/* AWAY Team */}
        <div className="flex items-center justify-end gap-3 md:gap-4 w-1/3">
          <span className="text-4xl md:text-5xl font-scoreboard text-white">{String(awayScore).padStart(2, '0')}</span>
          <span className="text-xl md:text-2xl font-bold text-rose-400">AWAY</span>
        </div>
      </div>

      <div className="flex justify-between items-center mt-2 px-1 text-xs md:text-sm text-gray-300">
        {/* HOME Details */}
        <div className="flex items-center gap-3 md:gap-4 w-1/3">
          <span className="font-semibold">Fouls: <span className="text-white">{homeFouls}</span></span>
          <TimeoutIndicator count={homeTimeouts} color="bg-cyan-400" />
        </div>

        {/* Center Spacer */}
        <div className="w-1/3"></div>

        {/* AWAY Details */}
        <div className="flex items-center justify-end gap-3 md:gap-4 w-1/3">
          <TimeoutIndicator count={awayTimeouts} color="bg-rose-400" />
          <span className="font-semibold">Fouls: <span className="text-white">{awayFouls}</span></span>
        </div>
      </div>
    </header>
  );
};

export default ScoreboardHeader;
