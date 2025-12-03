import React, { useState, useEffect, useRef } from 'react';
import { 
  ClipboardList, 
  UserPlus, 
  Trash2, 
  Download, 
  Upload,
  Trophy, 
  Activity, 
  Search, 
  ChevronDown, 
  ChevronUp,
  Save,
  X,
  GraduationCap,
  BarChart3,
  ArrowUpDown,
  User,
  Filter,
  AlertTriangle
} from 'lucide-react';

// --- Constants & Config ---

const SKILLS = [
  { id: 'hitting', label: 'Hitting' },
  { id: 'passing', label: 'Passing' },
  { id: 'defense', label: 'Defense' },
  { id: 'setting', label: 'Setting' },
  { id: 'serving', label: 'Serving' },
  { id: 'voice', label: 'Voice/Presence' },
  { id: 'potential', label: 'Potential to Improve' }
];

const POSITIONS = [
  "Outside", 
  "Middle", 
  "Right Side", 
  "Setter", 
  "Libero/DS"
];

const GRADES = ['7', '8', '9', '10', '11', '12'];

const MAX_SCORE = 10;
const MIN_SCORE = 0; 

const INITIAL_FORM_STATE = {
  id: null, // null means new player
  firstName: '',
  lastName: '',
  number: '',
  grade: '',
  position: '',
  skills: SKILLS.reduce((acc, skill) => ({ ...acc, [skill.id]: 0 }), {}) 
};

// --- Components ---

const Header = ({ activeTab, setActiveTab }) => (
  <header className="bg-slate-900 text-white p-4 shadow-lg sticky top-0 z-50">
    <div className="max-w-5xl mx-auto flex flex-col sm:flex-row justify-between items-center gap-4 sm:gap-0">
      <div className="flex items-center space-x-2">
        <div className="bg-blue-500 p-2 rounded-lg">
          <Activity size={24} className="text-white" />
        </div>
        <div>
          <h1 className="text-xl font-bold tracking-tight">HAWK-EYE</h1>
          <p className="text-xs text-slate-400 uppercase tracking-widest">Volleyball Eval</p>
        </div>
      </div>
      
      <div className="flex bg-slate-800 rounded-lg p-1 w-full sm:w-auto">
        <button
          onClick={() => setActiveTab('eval')}
          className={`flex-1 sm:flex-none flex items-center justify-center space-x-1 px-4 py-2 rounded-md text-sm font-medium transition-all ${
            activeTab === 'eval' 
              ? 'bg-blue-600 text-white shadow' 
              : 'text-slate-400 hover:text-white'
          }`}
        >
          <UserPlus size={16} className="mr-1" /> Eval
        </button>
        <button
          onClick={() => setActiveTab('results')}
          className={`flex-1 sm:flex-none flex items-center justify-center space-x-1 px-4 py-2 rounded-md text-sm font-medium transition-all ${
            activeTab === 'results' 
              ? 'bg-blue-600 text-white shadow' 
              : 'text-slate-400 hover:text-white'
          }`}
        >
          <ClipboardList size={16} className="mr-1" /> Data
        </button>
        <button
          onClick={() => setActiveTab('reports')}
          className={`flex-1 sm:flex-none flex items-center justify-center space-x-1 px-4 py-2 rounded-md text-sm font-medium transition-all ${
            activeTab === 'reports' 
              ? 'bg-blue-600 text-white shadow' 
              : 'text-slate-400 hover:text-white'
          }`}
        >
          <BarChart3 size={16} className="mr-1" /> Reports
        </button>
      </div>
    </div>
  </header>
);

const ScoreSlider = ({ skill, value, onChange }) => {
  const getScoreColor = (s) => {
    if (s >= 8) return 'text-green-600 font-bold';
    if (s >= 5) return 'text-blue-600 font-semibold';
    if (s > 0) return 'text-slate-700 font-medium';
    return 'text-slate-400';
  };

  return (
    <div className="mb-6 bg-white p-4 rounded-xl shadow-sm border border-slate-100">
      <div className="flex justify-between items-center mb-2">
        <label className="text-sm font-bold text-slate-700 uppercase tracking-wide">
          {skill.label}
        </label>
        <span className={`text-xl ${getScoreColor(value)}`}>{value}</span>
      </div>
      <input
        type="range"
        min={MIN_SCORE}
        max={MAX_SCORE}
        value={value}
        onChange={(e) => onChange(skill.id, parseInt(e.target.value))}
        className="w-full h-3 bg-slate-200 rounded-lg appearance-none cursor-pointer accent-blue-600 hover:accent-blue-500 transition-all"
      />
      <div className="flex justify-between text-xs text-slate-400 mt-1">
        <span>Needs Work ({MIN_SCORE})</span>
        <span>Elite ({MAX_SCORE})</span>
      </div>
    </div>
  );
};

const PlayerCard = ({ player, onDelete, minimal = false }) => {
  const [expanded, setExpanded] = useState(false);

  const scores = Object.values(player.skills);
  const total = scores.reduce((a, b) => a + b, 0);
  const potential = player.skills.potential;

  return (
    <div className="bg-white rounded-xl shadow-sm border border-slate-200 mb-4 overflow-hidden hover:shadow-md transition-shadow">
      <div 
        className="p-4 flex items-center justify-between cursor-pointer"
        onClick={() => setExpanded(!expanded)}
      >
        <div className="flex items-center space-x-4">
          <div className="flex flex-col items-center justify-center w-12 h-12 bg-slate-100 rounded-full text-slate-700 font-bold border-2 border-slate-200 shadow-sm shrink-0">
            <span className="text-[10px] text-slate-400 leading-none">#</span>
            <span className="text-lg leading-none">{player.number}</span>
          </div>
          <div>
            <h3 className="font-bold text-lg text-slate-800 leading-tight">{player.firstName} {player.lastName}</h3>
            <div className="flex flex-wrap items-center gap-2 text-xs text-slate-500 mt-1">
               <span className="bg-blue-50 text-blue-700 px-2 py-0.5 rounded font-medium border border-blue-100">
                {player.position || 'N/A'}
              </span>
              <span className="flex items-center text-slate-500 bg-slate-100 px-2 py-0.5 rounded border border-slate-200">
                <GraduationCap size={12} className="mr-1" />
                Gr: {player.grade || '-'}
              </span>
            </div>
          </div>
        </div>
        
        <div className="flex items-center space-x-4 text-right">
          <div className="hidden sm:block">
            <div className="text-xs text-slate-400 uppercase tracking-wider font-semibold">Total</div>
            <div className="text-xl font-bold text-blue-600">{total}</div>
          </div>
          <div className="hidden sm:block">
            <div className={`text-xs font-bold px-2 py-1 rounded ${potential >= 8 ? 'bg-green-100 text-green-700' : 'bg-slate-100 text-slate-500'}`}>
              Pot: {potential}
            </div>
          </div>
          {expanded ? <ChevronUp size={20} className="text-slate-400" /> : <ChevronDown size={20} className="text-slate-400" />}
        </div>
      </div>

      {expanded && (
        <div className="px-4 pb-4 pt-0 bg-slate-50 border-t border-slate-100">
          <div className="grid grid-cols-2 sm:grid-cols-4 gap-2 mt-4">
            {SKILLS.map((skill) => (
              <div key={skill.id} className="flex justify-between text-xs sm:text-sm p-2 bg-white rounded border border-slate-100 shadow-sm">
                <span className="text-slate-500 font-medium truncate mr-2">{skill.label}</span>
                <span className="font-bold text-slate-800">{player.skills[skill.id]}</span>
              </div>
            ))}
          </div>
          {!minimal && (
            <div className="mt-4 flex justify-between items-center pt-2 border-t border-slate-200">
              <div className="text-xs text-slate-400">
                ID: {player.id.toString().slice(-6)}
              </div>
              <button 
                onClick={(e) => {
                  e.stopPropagation();
                  onDelete(player.id);
                }}
                className="flex items-center text-red-500 hover:text-red-700 text-sm font-medium px-3 py-1 rounded hover:bg-red-50 transition-colors"
              >
                <Trash2 size={16} className="mr-1" /> Delete
              </button>
            </div>
          )}
        </div>
      )}
    </div>
  );
};

const ConfirmModal = ({ isOpen, title, message, onConfirm, onCancel }) => {
  if (!isOpen) return null;
  return (
    <div className="fixed inset-0 bg-black bg-opacity-50 z-[60] flex items-center justify-center p-4 animate-fade-in">
      <div className="bg-white rounded-xl shadow-2xl max-w-sm w-full p-6">
        <div className="flex items-center space-x-3 mb-4 text-amber-500">
          <AlertTriangle size={32} />
          <h3 className="text-xl font-bold text-slate-800">{title}</h3>
        </div>
        <p className="text-slate-600 mb-6">{message}</p>
        <div className="flex space-x-3">
          <button 
            onClick={onCancel}
            className="flex-1 px-4 py-2 bg-slate-100 hover:bg-slate-200 text-slate-700 rounded-lg font-medium transition-colors"
          >
            Cancel
          </button>
          <button 
            onClick={onConfirm}
            className="flex-1 px-4 py-2 bg-red-600 hover:bg-red-700 text-white rounded-lg font-medium transition-colors"
          >
            Confirm
          </button>
        </div>
      </div>
    </div>
  );
};

// --- Main Application ---

export default function App() {
  const [activeTab, setActiveTab] = useState('eval');
  const [players, setPlayers] = useState([]);
  
  // Sorting & Data State
  const [resultSort, setResultSort] = useState('score');
  const [reportType, setReportType] = useState('overall');
  const [formData, setFormData] = useState(INITIAL_FORM_STATE);
  
  // Eval Filter State
  const [filterMode, setFilterMode] = useState('all'); // 'all', 'grade', 'position'
  const [filterValue, setFilterValue] = useState('');

  // UI State
  const [notification, setNotification] = useState(null);
  const [searchTerm, setSearchTerm] = useState('');
  const fileInputRef = useRef(null);
  
  // Modal State
  const [confirmModal, setConfirmModal] = useState({ 
    isOpen: false, 
    title: '', 
    message: '', 
    action: null 
  });

  // Load from local storage
  useEffect(() => {
    const saved = localStorage.getItem('hawkeye_data');
    if (saved) {
      try {
        setPlayers(JSON.parse(saved));
      } catch (e) {
        console.error("Failed to load data", e);
      }
    }
  }, []);

  // Save to local storage
  useEffect(() => {
    localStorage.setItem('hawkeye_data', JSON.stringify(players));
  }, [players]);

  const handleSkillChange = (skillId, value) => {
    setFormData(prev => ({
      ...prev,
      skills: { ...prev.skills, [skillId]: value }
    }));
  };

  const handleInputChange = (e) => {
    const { name, value } = e.target;
    setFormData(prev => ({ ...prev, [name]: value }));
  };

  const handlePlayerSelect = (e) => {
    const playerId = parseInt(e.target.value);
    if (!playerId) {
      setFormData(INITIAL_FORM_STATE);
      return;
    }
    const player = players.find(p => p.id === playerId);
    if (player) {
      setFormData(player);
    }
  };

  const handleFilterModeChange = (mode) => {
    setFilterMode(mode);
    setFilterValue(''); // Reset specific filter when mode changes
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    if (!formData.firstName || !formData.lastName || !formData.number) {
      showNotification('Please enter full name and jersey number', 'error');
      return;
    }

    if (formData.id) {
      // Update Existing Player
      setPlayers(prev => prev.map(p => 
        p.id === formData.id 
          ? { ...formData, timestamp: new Date().toISOString() } 
          : p
      ));
      showNotification('Evaluation updated!', 'success');
    } else {
      // Create New Player
      const newPlayer = {
        ...formData,
        id: Date.now(),
        timestamp: new Date().toISOString()
      };
      setPlayers(prev => [newPlayer, ...prev]);
      showNotification('Player added successfully!', 'success');
    }
    
    // Reset form
    setFormData(INITIAL_FORM_STATE);
    window.scrollTo({ top: 0, behavior: 'smooth' });
  };

  // --- Modal & Delete Logic ---

  const initiateDelete = (id) => {
    setConfirmModal({
      isOpen: true,
      title: 'Delete Evaluation?',
      message: 'This will permanently remove this player\'s evaluation data. This action cannot be undone.',
      action: () => {
        setPlayers(prev => prev.filter(p => p.id !== id));
        showNotification('Player deleted.', 'success');
        setConfirmModal({ isOpen: false, title: '', message: '', action: null });
      }
    });
  };

  const initiateReset = () => {
    setConfirmModal({
      isOpen: true,
      title: 'Reset All Data?',
      message: 'WARNING: This will wipe ALL player data and evaluations. Ensure you have exported a CSV backup before proceeding.',
      action: () => {
        setPlayers([]);
        showNotification('All data cleared.', 'success');
        setConfirmModal({ isOpen: false, title: '', message: '', action: null });
      }
    });
  };

  // --- Helpers ---

  const getPlayerScore = (p) => Object.values(p.skills).reduce((x, y) => x + y, 0);

  const generateCSV = (dataList, filename) => {
    if (dataList.length === 0) return;

    const headers = [
      'First Name', 
      'Last Name', 
      'Number', 
      'Grade', 
      'Position', 
      ...SKILLS.map(s => s.label), 
      'Total Score', 
      'Average'
    ];
    
    const rows = dataList.map(p => {
      const scores = SKILLS.map(s => p.skills[s.id]);
      const total = scores.reduce((a, b) => a + b, 0);
      const avg = (total / scores.length).toFixed(2);
      return [
        `"${p.firstName}"`, 
        `"${p.lastName}"`, 
        p.number,
        `"${p.grade || ''}"`,
        `"${p.position || ''}"`,
        ...scores, 
        total, 
        avg
      ].join(',');
    });

    const csvContent = [headers.join(','), ...rows].join('\n');
    const blob = new Blob([csvContent], { type: 'text/csv;charset=utf-8;' });
    const url = URL.createObjectURL(blob);
    const link = document.createElement('a');
    link.setAttribute('href', url);
    link.setAttribute('download', `${filename}_${new Date().toLocaleDateString()}.csv`);
    document.body.appendChild(link);
    link.click();
    document.body.removeChild(link);
  };

  const handleBulkImport = (e) => {
    const file = e.target.files[0];
    if (!file) return;

    const reader = new FileReader();
    reader.onload = (event) => {
      try {
        const text = event.target.result;
        const lines = text.split('\n');
        const newPlayers = [];
        
        for (let i = 1; i < lines.length; i++) {
          const line = lines[i].trim();
          if (!line) continue;
          
          const cols = line.split(',').map(c => c.replace(/"/g, '').trim());
          
          if (cols.length >= 3) {
            newPlayers.push({
              id: Date.now() + i,
              firstName: cols[0] || 'Unknown',
              lastName: cols[1] || 'Unknown',
              number: cols[2] || '0',
              grade: cols[3] || '',
              position: cols[4] || '',
              skills: SKILLS.reduce((acc, skill) => ({ ...acc, [skill.id]: 0 }), {}), 
              timestamp: new Date().toISOString()
            });
          }
        }

        if (newPlayers.length > 0) {
          setPlayers(prev => [...newPlayers, ...prev]);
          showNotification(`Imported ${newPlayers.length} players!`, 'success');
        } else {
          showNotification('No valid player data found', 'error');
        }
      } catch (err) {
        console.error(err);
        showNotification('Failed to parse CSV file', 'error');
      }
    };
    reader.readAsText(file);
    e.target.value = '';
  };

  const showNotification = (msg, type) => {
    setNotification({ msg, type });
    setTimeout(() => setNotification(null), 3000);
  };

  // --- Sorting & Filtering Logic ---

  const getSortedPlayers = (list, sortType) => {
    let sorted = [...list];
    
    // Filter
    if (searchTerm) {
      const lowerTerm = searchTerm.toLowerCase();
      sorted = sorted.filter(p => 
        p.firstName?.toLowerCase().includes(lowerTerm) || 
        p.lastName?.toLowerCase().includes(lowerTerm) ||
        p.number.includes(lowerTerm)
      );
    }

    // Sort
    switch (sortType) {
      case 'name':
        return sorted.sort((a, b) => a.lastName.localeCompare(b.lastName));
      
      case 'grade':
        return sorted.sort((a, b) => {
          const gradeA = parseInt(a.grade) || 0;
          const gradeB = parseInt(b.grade) || 0;
          if (gradeA !== gradeB) return gradeA - gradeB;
          return getPlayerScore(b) - getPlayerScore(a);
        });

      case 'position':
        return sorted.sort((a, b) => {
          const posA = (a.position || 'Z').toString();
          const posB = (b.position || 'Z').toString();
          const posCompare = posA.localeCompare(posB);
          if (posCompare !== 0) return posCompare;
          return getPlayerScore(b) - getPlayerScore(a);
        });

      case 'score':
      default:
        return sorted.sort((a, b) => getPlayerScore(b) - getPlayerScore(a));
    }
  };

  const resultsData = getSortedPlayers(players, resultSort);
  const reportData = getSortedPlayers(players, reportType === 'overall' ? 'score' : reportType);

  const currentTotal = Object.values(formData.skills).reduce((a, b) => a + b, 0);

  // Helper to render filtered options
  const renderPlayerOptions = () => {
    let filteredPlayers = [...players].sort((a,b) => a.lastName.localeCompare(b.lastName));

    // Filter Logic
    if (filterMode === 'grade' && filterValue) {
        filteredPlayers = filteredPlayers.filter(p => (p.grade || '').toString() === filterValue);
    } else if (filterMode === 'position' && filterValue) {
        filteredPlayers = filteredPlayers.filter(p => (p.position || '') === filterValue);
    }

    // Edge Cases for UX
    if (filterMode !== 'all' && !filterValue) {
        return <option disabled>Select a specific {filterMode} above...</option>;
    }

    if (filteredPlayers.length === 0) {
        return <option disabled>No players found in this group</option>;
    }

    return filteredPlayers.map(p => (
        <option key={p.id} value={p.id}>
          {p.lastName}, {p.firstName} (#{p.number})
        </option>
    ));
  };

  return (
    <div className="min-h-screen bg-slate-50 font-sans text-slate-900 pb-20">
      <Header activeTab={activeTab} setActiveTab={setActiveTab} />

      {notification && (
        <div className={`fixed top-20 left-1/2 transform -translate-x-1/2 px-6 py-3 rounded-full shadow-xl z-50 flex items-center space-x-2 animate-bounce ${
          notification.type === 'error' ? 'bg-red-500 text-white' : 'bg-green-500 text-white'
        }`}>
          {notification.type === 'success' ? <Save size={18} /> : <X size={18} />}
          <span className="font-medium">{notification.msg}</span>
        </div>
      )}

      {/* Custom Confirmation Modal */}
      <ConfirmModal 
        isOpen={confirmModal.isOpen}
        title={confirmModal.title}
        message={confirmModal.message}
        onConfirm={confirmModal.action}
        onCancel={() => setConfirmModal({ ...confirmModal, isOpen: false })}
      />

      <main className="max-w-md mx-auto p-4 md:max-w-4xl">
        
        {/* EVALUATION VIEW */}
        {activeTab === 'eval' && (
          <div className="animate-fade-in">
            <div className="mb-6 text-center">
              <h2 className="text-2xl font-bold text-slate-800">
                {formData.id ? 'Edit Evaluation' : 'New Evaluation'}
              </h2>
              <p className="text-slate-500">Score skills and enter details</p>
            </div>

            {/* Select Player Dropdown */}
            <div className="bg-white p-4 rounded-xl shadow-sm border border-slate-200 mb-6">
               <div className="flex flex-col space-y-3 mb-3">
                 <div className="flex justify-between items-center">
                     <label className="text-xs font-bold text-slate-500 uppercase tracking-wide flex items-center">
                       <User size={14} className="mr-1" /> Select Player
                     </label>
                     
                     <div className="flex items-center space-x-1 bg-slate-50 p-1 rounded-lg border border-slate-100">
                       <span className="text-[10px] text-slate-400 font-bold uppercase px-1 hidden sm:inline">Filter By:</span>
                       {['all', 'grade', 'position'].map(mode => (
                          <button 
                            key={mode}
                            onClick={() => handleFilterModeChange(mode)}
                            className={`px-3 py-1 text-[10px] font-bold uppercase rounded transition-all ${
                              filterMode === mode 
                                ? 'bg-white shadow text-blue-600 border border-slate-100' 
                                : 'text-slate-400 hover:text-slate-600 hover:bg-slate-100'
                            }`}
                          >
                            {mode === 'all' ? 'All' : mode === 'position' ? 'Pos' : mode}
                          </button>
                       ))}
                     </div>
                 </div>

                 {/* Secondary Filter Dropdowns */}
                 {filterMode === 'grade' && (
                    <select 
                        value={filterValue}
                        onChange={(e) => setFilterValue(e.target.value)}
                        className="w-full p-2 bg-blue-50 border border-blue-100 rounded-lg text-sm font-bold text-blue-700 focus:ring-2 focus:ring-blue-500 outline-none"
                    >
                        <option value="">-- Select Grade --</option>
                        {GRADES.map(g => <option key={g} value={g}>Grade {g}</option>)}
                    </select>
                 )}

                 {filterMode === 'position' && (
                    <select 
                        value={filterValue}
                        onChange={(e) => setFilterValue(e.target.value)}
                        className="w-full p-2 bg-blue-50 border border-blue-100 rounded-lg text-sm font-bold text-blue-700 focus:ring-2 focus:ring-blue-500 outline-none"
                    >
                        <option value="">-- Select Position --</option>
                        {POSITIONS.map(p => <option key={p} value={p}>{p}</option>)}
                    </select>
                 )}
               </div>
               
               <div className="relative">
                 <select
                   className="w-full p-3 bg-slate-50 border border-slate-200 rounded-lg focus:ring-2 focus:ring-blue-500 focus:outline-none text-slate-800 appearance-none disabled:bg-slate-100 disabled:text-slate-400"
                   onChange={handlePlayerSelect}
                   value={formData.id || ''}
                 >
                   <option value="">-- Create New Player --</option>
                   {renderPlayerOptions()}
                 </select>
                 <ChevronDown className="absolute right-3 top-1/2 transform -translate-y-1/2 text-slate-400 pointer-events-none" size={16} />
               </div>
            </div>

            <form onSubmit={handleSubmit} className="space-y-6">
              <div className="bg-white p-6 rounded-xl shadow-sm border border-slate-200 grid grid-cols-2 gap-4">
                
                {/* Name Fields */}
                <div className="col-span-1">
                  <label className="block text-sm font-bold text-slate-700 mb-2">First Name</label>
                  <input
                    type="text"
                    name="firstName"
                    value={formData.firstName}
                    onChange={handleInputChange}
                    placeholder="Jane"
                    className="w-full p-3 bg-slate-50 border border-slate-200 rounded-lg focus:ring-2 focus:ring-blue-500 focus:outline-none"
                  />
                </div>
                <div className="col-span-1">
                  <label className="block text-sm font-bold text-slate-700 mb-2">Last Name</label>
                  <input
                    type="text"
                    name="lastName"
                    value={formData.lastName}
                    onChange={handleInputChange}
                    placeholder="Doe"
                    className="w-full p-3 bg-slate-50 border border-slate-200 rounded-lg focus:ring-2 focus:ring-blue-500 focus:outline-none"
                  />
                </div>

                {/* Number & Grade */}
                <div className="col-span-1">
                  <label className="block text-sm font-bold text-slate-700 mb-2">Jersey #</label>
                  <input
                    type="number"
                    name="number"
                    value={formData.number}
                    onChange={handleInputChange}
                    placeholder="10"
                    className="w-full p-3 bg-slate-50 border border-slate-200 rounded-lg focus:ring-2 focus:ring-blue-500 focus:outline-none text-center"
                  />
                </div>
                <div className="col-span-1">
                  <label className="block text-sm font-bold text-slate-700 mb-2">Grade</label>
                  <select
                    name="grade"
                    value={formData.grade}
                    onChange={handleInputChange}
                    className="w-full p-3 bg-slate-50 border border-slate-200 rounded-lg focus:ring-2 focus:ring-blue-500 focus:outline-none"
                  >
                    <option value="">Select...</option>
                    {GRADES.map(g => (
                      <option key={g} value={g}>{g}</option>
                    ))}
                  </select>
                </div>

                {/* Position */}
                <div className="col-span-2">
                  <label className="block text-sm font-bold text-slate-700 mb-2">Position</label>
                  <select
                    name="position"
                    value={formData.position}
                    onChange={handleInputChange}
                    className="w-full p-3 bg-slate-50 border border-slate-200 rounded-lg focus:ring-2 focus:ring-blue-500 focus:outline-none"
                  >
                    <option value="">-- Select Position --</option>
                    {POSITIONS.map(pos => (
                      <option key={pos} value={pos}>{pos}</option>
                    ))}
                  </select>
                </div>
              </div>

              {/* Total Score Display */}
              <div className="bg-slate-800 text-white p-4 rounded-xl shadow-lg flex justify-between items-center sticky top-20 z-40">
                <div className="flex items-center space-x-2">
                  <Trophy size={20} className="text-yellow-400" />
                  <span className="font-bold text-lg">Total Score</span>
                </div>
                <div className="flex items-baseline space-x-1">
                  <span className="text-3xl font-bold text-blue-400">{currentTotal}</span>
                  <span className="text-sm text-slate-400">/ {SKILLS.length * MAX_SCORE}</span>
                </div>
              </div>

              <div className="space-y-4">
                {SKILLS.map((skill) => (
                  <ScoreSlider 
                    key={skill.id} 
                    skill={skill} 
                    value={formData.skills[skill.id]} 
                    onChange={handleSkillChange} 
                  />
                ))}
              </div>

              <button
                type="submit"
                className="w-full bg-blue-600 hover:bg-blue-700 text-white font-bold py-4 rounded-xl shadow-lg hover:shadow-xl transition-all flex justify-center items-center space-x-2 text-lg"
              >
                {formData.id ? <Save size={24} /> : <UserPlus size={24} />}
                <span>{formData.id ? 'Update Evaluation' : 'Save Evaluation'}</span>
              </button>
            </form>
          </div>
        )}

        {/* RESULTS / DATA MANAGEMENT VIEW */}
        {activeTab === 'results' && (
          <div className="animate-fade-in">
            <div className="flex flex-col md:flex-row md:items-center justify-between mb-6 gap-4">
              <div>
                <h2 className="text-2xl font-bold text-slate-800">Player Data</h2>
                <p className="text-slate-500">Manage roster and export data</p>
              </div>
              <div className="flex flex-wrap gap-2">
                <input 
                  type="file" 
                  ref={fileInputRef}
                  onChange={handleBulkImport}
                  accept=".csv"
                  className="hidden" 
                />
                <button onClick={() => fileInputRef.current.click()} className="flex items-center justify-center space-x-2 bg-slate-600 hover:bg-slate-700 text-white px-3 py-2 rounded-lg text-sm font-medium transition-colors">
                  <Upload size={16} /> <span className="hidden sm:inline">Import</span>
                </button>
                 <button onClick={() => generateCSV(players, 'hawkeye_full_data')} disabled={players.length === 0} className="flex items-center justify-center space-x-2 bg-emerald-600 hover:bg-emerald-700 text-white px-3 py-2 rounded-lg text-sm font-medium transition-colors disabled:opacity-50">
                  <Download size={16} /> <span className="hidden sm:inline">Export</span>
                </button>
                <button onClick={initiateReset} disabled={players.length === 0} className="px-3 py-2 text-red-500 hover:bg-red-50 rounded-lg text-sm font-medium transition-colors border border-transparent hover:border-red-100">
                  Reset
                </button>
              </div>
            </div>

            {/* Sort Controls */}
            <div className="bg-white p-3 rounded-lg shadow-sm border border-slate-200 mb-4 flex flex-col sm:flex-row items-start sm:items-center gap-2">
               <span className="text-xs font-bold text-slate-500 uppercase mr-2 flex items-center">
                 <ArrowUpDown size={14} className="mr-1" /> Sort By:
               </span>
               <div className="flex flex-wrap gap-2 w-full">
                 {['score', 'name', 'grade', 'position'].map(type => (
                   <button
                    key={type}
                    onClick={() => setResultSort(type)}
                    className={`px-3 py-1.5 rounded text-xs font-bold uppercase tracking-wide transition-all ${
                      resultSort === type 
                        ? 'bg-blue-600 text-white shadow-md' 
                        : 'bg-slate-100 text-slate-500 hover:bg-slate-200'
                    }`}
                   >
                     {type}
                   </button>
                 ))}
               </div>
            </div>

            <div className="relative mb-6">
              <Search className="absolute left-3 top-1/2 transform -translate-y-1/2 text-slate-400" size={20} />
              <input 
                type="text" 
                placeholder="Search players..." 
                value={searchTerm}
                onChange={(e) => setSearchTerm(e.target.value)}
                className="w-full pl-10 p-3 bg-white border border-slate-200 rounded-lg shadow-sm focus:ring-2 focus:ring-blue-500 focus:outline-none"
              />
            </div>

            <div className="space-y-4">
              {resultsData.length > 0 ? (
                resultsData.map((player, index) => (
                  <PlayerCard 
                    key={player.id} 
                    player={player} 
                    rank={index + 1} 
                    onDelete={initiateDelete} 
                  />
                ))
              ) : (
                <div className="text-center py-20 bg-white rounded-xl border border-dashed border-slate-300">
                  <ClipboardList size={48} className="mx-auto text-slate-300 mb-4" />
                  <p className="text-slate-500 font-medium">No players found.</p>
                </div>
              )}
            </div>
          </div>
        )}

        {/* REPORTS VIEW */}
        {activeTab === 'reports' && (
          <div className="animate-fade-in">
            <div className="flex flex-col md:flex-row md:items-center justify-between mb-6 gap-4">
              <div>
                <h2 className="text-2xl font-bold text-slate-800">Reports</h2>
                <p className="text-slate-500">View and export ranked lists</p>
              </div>
              <button
                onClick={() => generateCSV(reportData, `hawkeye_report_${reportType}`)}
                disabled={reportData.length === 0}
                className="flex items-center justify-center space-x-2 bg-blue-600 hover:bg-blue-700 text-white px-4 py-2 rounded-lg font-medium transition-colors disabled:opacity-50"
              >
                <Download size={18} />
                <span>Export This Report</span>
              </button>
            </div>

            {/* Report Controls */}
            <div className="bg-white p-4 rounded-xl shadow-sm border border-slate-200 mb-6">
              <label className="block text-xs font-bold text-slate-500 uppercase tracking-wide mb-2">
                Select Report Type
              </label>
              <div className="flex flex-wrap gap-2">
                <button
                  onClick={() => setReportType('overall')}
                  className={`flex-1 px-4 py-2 rounded-lg text-sm font-medium border transition-all ${
                    reportType === 'overall'
                      ? 'bg-blue-50 border-blue-200 text-blue-700'
                      : 'bg-white border-slate-200 text-slate-600 hover:bg-slate-50'
                  }`}
                >
                  1. Overall Rank
                </button>
                <button
                  onClick={() => setReportType('grade')}
                  className={`flex-1 px-4 py-2 rounded-lg text-sm font-medium border transition-all ${
                    reportType === 'grade'
                      ? 'bg-blue-50 border-blue-200 text-blue-700'
                      : 'bg-white border-slate-200 text-slate-600 hover:bg-slate-50'
                  }`}
                >
                  2. By Grade
                </button>
                <button
                  onClick={() => setReportType('position')}
                  className={`flex-1 px-4 py-2 rounded-lg text-sm font-medium border transition-all ${
                    reportType === 'position'
                      ? 'bg-blue-50 border-blue-200 text-blue-700'
                      : 'bg-white border-slate-200 text-slate-600 hover:bg-slate-50'
                  }`}
                >
                  3. By Position
                </button>
              </div>
            </div>

            {/* Report List */}
            <div className="space-y-3">
              <h3 className="text-sm font-bold text-slate-400 uppercase tracking-wider mb-2">
                {reportType === 'overall' && "Highest Score to Lowest"}
                {reportType === 'grade' && "Ranked by Grade (7-12), then Score"}
                {reportType === 'position' && "Ranked by Position (A-Z), then Score"}
              </h3>

              {reportData.length > 0 ? (
                reportData.map((player, index) => (
                  <div key={player.id} className="bg-white p-3 rounded-lg border border-slate-100 flex items-center justify-between">
                    <div className="flex items-center space-x-3">
                      <div className="text-slate-400 font-mono text-sm w-6">{index + 1}</div>
                      <div>
                        <div className="font-bold text-slate-800">{player.firstName} {player.lastName}</div>
                        <div className="text-xs text-slate-500 flex space-x-2">
                           {reportType === 'grade' && <span className="text-blue-600 font-bold">Gr: {player.grade}</span>}
                           {reportType === 'position' && <span className="text-blue-600 font-bold">{player.position}</span>}
                           {reportType === 'overall' && <span>{player.position} • Gr {player.grade}</span>}
                        </div>
                      </div>
                    </div>
                    <div className="text-right">
                       <div className="text-lg font-bold text-slate-800">{getPlayerScore(player)}</div>
                       <div className="text-[10px] text-slate-400">Total Pts</div>
                    </div>
                  </div>
                ))
              ) : (
                <div className="text-center py-10 text-slate-400">No data available for this report.</div>
              )}
            </div>
          </div>
        )}

      </main>
    </div>
  );
}
