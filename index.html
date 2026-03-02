import React, { useState, useMemo, useEffect, useRef } from 'react';
import { 
  PlusCircle, 
  Trash2, 
  MapPin, 
  Ship,
  Briefcase,
  Loader2,
  Edit2,
  X,
  Save,
  Archive,
  BarChart3,
  Printer,
  FileSpreadsheet,
  FolderPlus,
  ArrowLeft,
  CheckCircle2,
  AlertCircle,
  Tag,
  FileText,
  Eye,
  ChevronRight
} from 'lucide-react';

// Firebase SDK - 데이터 저장을 위해 필요합니다.
import { initializeApp } from 'firebase/app';
import { getAuth, signInAnonymously, signInWithCustomToken, onAuthStateChanged } from 'firebase/auth';
import { getFirestore, collection, doc, setDoc, getDoc, onSnapshot, addDoc, deleteDoc, writeBatch } from 'firebase/firestore';

// 설정 로드 (Canvas 환경 제공 변수)
const firebaseConfig = JSON.parse(__firebase_config);
const app = initializeApp(firebaseConfig);
const auth = getAuth(app);
const db = getFirestore(app);
const appId = typeof __app_id !== 'undefined' ? __app_id : 'default-app-id';

const VERSION = "v1.1.0";

// KOSTA 공식 로고 (엔지니어님이 보내주신 이미지와 동일하게 정밀 수정됨)
const KostaLogo = ({ className = "h-10" }) => (
  <div className={`flex flex-col items-start ${className}`}>
    <svg viewBox="0 0 400 100" className="h-full w-auto" fill="none" xmlns="http://www.w3.org/2000/svg">
      <text x="0" y="75" fontFamily="Arial Black, sans-serif" fontWeight="900" fontSize="85" fill="black" letterSpacing="-5">KOST</text>
      <g transform="translate(255, 0)">
        <path d="M0 80 L40 5 L40 80 H25 L25 50 H15 L15 80 H0Z" fill="black" />
        <path d="M40 5 L80 80 H55 L40 50 L40 5Z" fill="#D10A10" />
      </g>
    </svg>
    <div className="text-[10px] font-bold tracking-[0.2em] text-black -mt-2 ml-1 uppercase font-sans">
      Korea Ship Automation Service
    </div>
  </div>
);

const App = () => {
  const [user, setUser] = useState(null);
  const [expenses, setExpenses] = useState([]);
  const [savedReports, setSavedReports] = useState([]);
  const [isLoading, setIsLoading] = useState(true);
  const [saveStatus, setSaveStatus] = useState('idle');
  const [showArchive, setShowArchive] = useState(false);
  const [showAddForm, setShowAddForm] = useState(false);
  const [showConfirmModal, setShowConfirmModal] = useState(false);
  const [showExportMenu, setShowExportMenu] = useState(false);
  const [showPreview, setShowPreview] = useState(false);

  const getTodayDate = () => {
    const date = new Date();
    return `${date.getFullYear()}-${String(date.getMonth() + 1).padStart(2, '0')}-${String(date.getDate()).padStart(2, '0')}`;
  };

  const categoryPresets = {
    'Meals (식대)': ['Breakfast (아침)', 'Lunch (점심)', 'Dinner (저녁)', 'Snack (간식)', 'Client Dinner (회식)'],
    'Transport (교통)': ['Taxi (택시)', 'Subway (지하철)', 'Bus (버스)', 'Fuel (주유)', 'Parking (주차)'],
    'Hotel (숙박)': ['Hotel (호텔)', 'Airbnb (에어비앤비)'],
    'Flight (항공)': ['Ticket (항공권)', 'Extra Baggage (수하물)'],
    'Business (업무)': ['Supplies (소모품)', 'SIM Card (유심)', 'Tools (공구)'],
    'Others (기타)': ['Visa Fee (비자)', 'Insurance (보험)']
  };

  const currencyList = [
    { code: 'CNY', symbol: '¥', label: 'CNY (¥)', defaultRate: 190 },
    { code: 'USD', symbol: '$', label: 'USD ($)', defaultRate: 1350 },
    { code: 'EUR', symbol: '€', label: 'EUR (€)', defaultRate: 1450 },
    { code: 'JPY', symbol: '¥', label: 'JPY (¥)', defaultRate: 9 },
    { code: 'KRW', symbol: '₩', label: 'KRW (₩)', defaultRate: 1 }
  ];

  const regionalData = {
    'China': { currency: 'CNY', symbol: '¥', defaultRate: 190 },
    'USA': { currency: 'USD', symbol: '$', defaultRate: 1350 },
    'Japan': { currency: 'JPY', symbol: '¥', defaultRate: 9 },
    'Europe': { currency: 'EUR', symbol: '€', defaultRate: 1450 },
    'Korea': { currency: 'KRW', symbol: '₩', defaultRate: 1 },
  };

  const [tripInfo, setTripInfo] = useState({
    title: '', destination: 'China', detailedLocation: '',
    currency: 'CNY', symbol: '¥', startDate: getTodayDate(), endDate: getTodayDate()
  });

  const [formData, setFormData] = useState({
    date: getTodayDate(), category: 'Meals (식대)', amount: '', rate: '190',
    description: '', method: 'Credit Card', currency: 'CNY', symbol: '¥'
  });

  useEffect(() => {
    const initAuth = async () => {
      if (typeof __initial_auth_token !== 'undefined' && __initial_auth_token) {
        await signInWithCustomToken(auth, __initial_auth_token);
      } else {
        await signInAnonymously(auth);
      }
    };
    initAuth();
    const unsubscribe = onAuthStateChanged(auth, setUser);
    return () => unsubscribe();
  }, []);

  useEffect(() => {
    if (!user) return;
    const tripRef = doc(db, 'artifacts', appId, 'users', user.uid, 'settings', 'current_trip');
    getDoc(tripRef).then(snap => snap.exists() && setTripInfo(snap.data()));

    const expensesCol = collection(db, 'artifacts', appId, 'users', user.uid, 'expenses');
    const unsubscribeExp = onSnapshot(expensesCol, (snap) => {
      const data = snap.docs.map(d => ({ ...d.data(), id: d.id }));
      setExpenses(data.sort((a, b) => new Date(b.date) - new Date(a.date)));
      setIsLoading(false);
    }, (err) => console.error(err));

    const reportsCol = collection(db, 'artifacts', appId, 'users', user.uid, 'finalized_reports');
    const unsubscribeRep = onSnapshot(reportsCol, (snap) => {
      const data = snap.docs.map(d => ({ ...d.data(), id: d.id }));
      setSavedReports(data.sort((a, b) => new Date(b.savedAt) - new Date(a.savedAt)));
    }, (err) => console.error(err));

    return () => { unsubscribeExp(); unsubscribeRep(); };
  }, [user]);

  const handlePrintAction = () => {
    setShowExportMenu(false);
    setTimeout(() => window.print(), 300);
  };

  const finalizeAndReset = async () => {
    if (!user || expenses.length === 0) return;
    setSaveStatus('saving');
    try {
      const reportData = { ...tripInfo, items: expenses, totals, savedAt: new Date().toISOString() };
      await addDoc(collection(db, 'artifacts', appId, 'users', user.uid, 'finalized_reports'), reportData);
      const batch = writeBatch(db);
      expenses.forEach((exp) => batch.delete(doc(db, 'artifacts', appId, 'users', user.uid, 'expenses', exp.id)));
      await batch.commit();
      setTripInfo({ ...tripInfo, title: '' });
      setSaveStatus('success');
      setShowConfirmModal(false);
      setTimeout(() => { setSaveStatus('idle'); setShowArchive(true); }, 1500);
    } catch (e) { setSaveStatus('idle'); }
  };

  const addExpense = async (e) => {
    if (e) e.preventDefault();
    if (!user || !formData.amount) return;
    try {
      const rateVal = parseFloat(formData.rate);
      const amountVal = parseFloat(formData.amount);
      await addDoc(collection(db, 'artifacts', appId, 'users', user.uid, 'expenses'), {
        ...formData, amount: amountVal, rate: rateVal, krwAmount: Math.round(amountVal * rateVal), createdAt: new Date().toISOString()
      });
      setFormData(prev => ({ ...prev, amount: '', description: '' }));
      setShowAddForm(false);
    } catch (err) { console.error(err); }
  };

  const totals = useMemo(() => expenses.reduce((acc, i) => {
    if (i.currency === 'KRW') acc.domestic += Number(i.amount) || 0;
    else acc.overseas += Number(i.krwAmount) || 0;
    acc.krw += Number(i.krwAmount) || 0;
    return acc;
  }, { domestic: 0, overseas: 0, krw: 0 }), [expenses]);

  return (
    <div className="min-h-screen bg-slate-50 font-sans text-slate-900 overflow-x-hidden">
      <style>{`
        @media print {
          .no-print { display: none !important; }
          .print-only { display: block !important; }
          body { background: white !important; margin: 0; padding: 0; -webkit-print-color-adjust: exact; }
          @page { size: A4; margin: 15mm; }
          .report-header { border-bottom: 3px solid #000; padding-bottom: 15px; margin-bottom: 30px; display: flex; justify-content: space-between; align-items: flex-end; }
          table { width: 100%; border-collapse: collapse; font-size: 10px; margin-top: 15px; }
          th, td { border: 1px solid #ddd; padding: 10px; text-align: left; }
          th { background-color: #f8fafc; font-weight: bold; }
          .total-box { margin-top: 25px; padding: 20px; background-color: #f8fafc; text-align: right; border: 1px solid #ddd; }
          .sig-section { margin-top: 80px; display: flex; justify-content: space-between; padding: 0 40px; }
          .sig-box { width: 220px; text-align: center; border-top: 1.5px solid #000; padding-top: 10px; font-size: 11px; font-weight: bold; }
        }
        .print-only { display: none; }
      `}</style>

      {/* 🚢 선주 제출용 공식 리포트 양식 */}
      <div className="print-only font-sans">
        <div className="report-header">
           <KostaLogo className="h-14" />
           <div className="text-right">
             <h1 className="text-2xl font-black text-slate-900 uppercase italic">Travel Expense Report</h1>
             <p className="text-[10px] text-slate-400 font-bold uppercase mt-1">Ref: {VERSION} | Date: {new Date().toLocaleDateString()}</p>
           </div>
        </div>
        <div className="grid grid-cols-2 gap-4 text-[12px] mb-8 font-medium">
          <div className="space-y-1">
            <p><span className="text-slate-400 uppercase text-[9px] font-black mr-2">Vessel:</span> {tripInfo.title || "TBA"}</p>
            <p><span className="text-slate-400 uppercase text-[9px] font-black mr-2">Port:</span> {tripInfo.destination} ({tripInfo.detailedLocation || "Main Yard"})</p>
          </div>
          <div className="text-right space-y-1">
            <p><span className="text-slate-400 uppercase text-[9px] font-black mr-2">Period:</span> {tripInfo.startDate} ~ {tripInfo.endDate}</p>
            <p><span className="text-slate-400 uppercase text-[9px] font-black mr-2">Total Amount:</span> KRW {totals.krw.toLocaleString()}</p>
          </div>
        </div>
        <table>
          <thead>
            <tr><th>Date</th><th>Category</th><th>Local Amount</th><th>Rate</th><th>KRW Sum</th><th>Description</th></tr>
          </thead>
          <tbody>
            {expenses.map(item => (
              <tr key={item.id}>
                <td className="whitespace-nowrap">{item.date}</td><td>{item.category.split(' (')[0]}</td>
                <td>{item.symbol}{item.amount.toLocaleString()}</td><td>{item.rate}</td>
                <td className="font-bold">₩{item.krwAmount.toLocaleString()}</td><td>{item.description}</td>
              </tr>
            ))}
          </tbody>
        </table>
        <div className="total-box">
           <p className="text-[10px] font-black text-slate-500 uppercase tracking-widest mb-1 font-sans">Total Reimbursement Claim</p>
           <p className="text-3xl font-black text-slate-900 tracking-tighter italic font-sans">KRW {totals.krw.toLocaleString()}</p>
        </div>
        <div className="sig-section font-sans">
           <div className="sig-box uppercase font-sans">Authorized Service Engineer</div>
           <div className="sig-box uppercase font-sans">Master / Owner Representative</div>
        </div>
      </div>

      {/* 📱 모바일 메인 화면 */}
      <div className="no-print font-sans">
        <header className="bg-white p-4 sticky top-0 z-40 shadow-sm flex justify-between items-center border-b border-slate-100 font-sans">
          <div className="max-w-md mx-auto w-full flex justify-between items-center px-2 font-sans">
            <KostaLogo className="h-8 font-sans" />
            <div className="flex gap-2 relative font-sans">
              <button onClick={() => setShowExportMenu(!showExportMenu)} className="p-2 bg-slate-50 text-slate-600 rounded-xl active:scale-95 border border-slate-100 font-sans">
                <Printer size={18} />
              </button>
              {showExportMenu && (
                <>
                  <div className="fixed inset-0 z-40" onClick={() => setShowExportMenu(false)}></div>
                  <div className="absolute top-12 right-0 bg-white text-slate-800 rounded-2xl shadow-2xl p-2 w-56 border border-slate-100 z-50 animate-in fade-in slide-in-from-top-2 font-sans font-sans">
                    <button onClick={() => { setShowExportMenu(false); setShowPreview(true); }} className="w-full flex items-center gap-3 p-3 hover:bg-slate-50 rounded-xl text-xs font-bold font-sans">
                      <Eye size={16} className="text-blue-500 font-sans" /> 리포트 미리보기
                    </button>
                    <button onClick={handlePrintAction} className="w-full flex items-center gap-3 p-3 hover:bg-slate-50 rounded-xl text-xs font-bold font-sans">
                      <FileText size={16} className="text-indigo-500 font-sans" /> PDF 저장 / 인쇄
                    </button>
                  </div>
                </>
              )}
              <button onClick={() => setShowArchive(true)} className="p-2 bg-slate-50 text-slate-600 rounded-xl active:scale-95 border border-slate-100 font-sans">
                <Archive size={18} />
              </button>
            </div>
          </div>
        </header>

        <main className="max-w-md mx-auto p-4 pb-32 space-y-6 font-sans">
          <div className="grid grid-cols-2 gap-3 font-sans">
            <div className="bg-white p-5 rounded-[2rem] border border-slate-100 font-sans">
              <p className="text-[10px] font-black text-slate-300 uppercase mb-1 font-sans">Local (₩)</p>
              <p className="text-xl font-black text-slate-800 tracking-tight font-sans font-sans">₩{totals.domestic.toLocaleString()}</p>
            </div>
            <div className="bg-white p-5 rounded-[2rem] border border-slate-100 font-sans">
              <p className="text-[10px] font-black text-slate-300 uppercase mb-1 font-sans">Overseas (₩)</p>
              <p className="text-xl font-black text-slate-800 tracking-tight font-sans">₩{totals.overseas.toLocaleString()}</p>
            </div>
            <div className="col-span-2 bg-slate-900 p-7 rounded-[2.5rem] text-white flex justify-between items-center shadow-xl font-sans">
              <div className="font-sans">
                <p className="text-[10px] font-black text-white/40 uppercase mb-1 tracking-widest font-sans">Grand Total</p>
                <p className="text-3xl font-black italic tracking-tighter font-sans">₩{totals.krw.toLocaleString()}</p>
              </div>
              <BarChart3 size={28} className="text-red-500 font-sans" />
            </div>
          </div>

          <section className="bg-white p-6 rounded-[2.5rem] border border-slate-100 space-y-4 font-sans">
            <input type="text" className="w-full p-4 bg-slate-50 border border-slate-100 rounded-2xl text-sm font-bold outline-none font-sans" placeholder="Vessel or Project Name" value={tripInfo.title} onChange={e => setTripInfo({...tripInfo, title: e.target.value})} />
            <div className="grid grid-cols-2 gap-3 font-sans">
              <select className="w-full p-4 bg-slate-50 border border-slate-100 rounded-2xl text-xs font-black outline-none font-sans" value={tripInfo.destination} onChange={e => {
                const m = regionalData[e.target.value];
                setTripInfo({...tripInfo, destination: e.target.value, currency: m.currency, symbol: m.symbol});
              }}>
                {Object.keys(regionalData).map(k => <option key={k} value={k}>{k}</option>)}
              </select>
              <input type="text" className="w-full p-4 bg-slate-50 border border-slate-100 rounded-2xl text-xs font-bold outline-none font-sans" placeholder="Yard or Location" value={tripInfo.detailedLocation} onChange={e => setTripInfo({...tripInfo, detailedLocation: e.target.value})} />
            </div>
          </section>

          <section className="space-y-3 font-sans font-sans font-sans">
            {expenses.map((item) => (
              <div key={item.id} className="bg-white p-5 rounded-[2.5rem] border border-slate-100 flex justify-between items-center group transition-all active:scale-95 font-sans font-sans font-sans">
                <div className="text-left space-y-1 font-sans font-sans">
                  <div className="flex items-center gap-2 font-sans font-sans font-sans">
                    <span className="text-[10px] font-black text-red-600 bg-red-50 px-2 py-0.5 rounded-lg font-sans">{item.date}</span>
                    <span className="text-[10px] font-bold text-slate-400 uppercase italic font-sans">{item.category.split(' (')[0]}</span>
                  </div>
                  <p className="font-bold text-slate-800 text-sm font-sans font-sans">{item.description}</p>
                </div>
                <div className="text-right font-sans font-sans font-sans">
                   <p className="font-black text-slate-900 text-lg italic font-sans font-sans">₩{item.krwAmount.toLocaleString()}</p>
                   <button onClick={() => deleteDoc(doc(db, 'artifacts', appId, 'users', user.uid, 'expenses', item.id))} className="p-2 text-slate-200 hover:text-red-500 opacity-0 group-hover:opacity-100 font-sans"><Trash2 size={14}/></button>
                </div>
              </div>
            ))}
          </section>
        </main>

        <div className="fixed bottom-10 left-0 right-0 px-4 flex justify-center z-40 font-sans font-sans font-sans">
          <button onClick={() => setShowAddForm(true)} className="px-14 py-5 bg-slate-900 text-white rounded-[2.5rem] font-black shadow-2xl tracking-widest uppercase text-sm italic active:scale-95 transition-all font-sans">Add Expense</button>
        </div>
      </div>

      {/* 🖼️ 리포트 미리보기 모달 */}
      {showPreview && (
        <div className="fixed inset-0 z-[100] bg-slate-900/95 overflow-y-auto font-sans flex flex-col items-center p-4 py-12 md:p-12 font-sans font-sans font-sans">
          <div className="bg-white w-full max-w-[210mm] min-h-[297mm] p-10 md:p-16 relative animate-in zoom-in-95 shadow-2xl font-sans font-sans font-sans">
            <button onClick={() => setShowPreview(false)} className="absolute -top-10 left-0 text-white font-bold flex items-center gap-2 font-sans">
              <ArrowLeft size={18} /> Back to Edit
            </button>
            <div className="report-header border-b-4 border-slate-900 pb-4 mb-8 font-sans font-sans">
              <KostaLogo className="h-14 font-sans font-sans font-sans" />
              <div className="text-right font-sans">
                <h1 className="text-2xl font-black text-slate-900 uppercase italic font-sans">Travel Expense Report</h1>
                <p className="text-[10px] font-bold text-slate-400 mt-1 uppercase font-sans">Official Service Documentation</p>
              </div>
            </div>
            <table className="font-sans font-sans font-sans">
              <thead>
                <tr className="bg-slate-50 border-y-2 border-slate-900 font-sans font-sans">
                  <th className="p-3">Date</th><th className="p-3">Category</th><th className="p-3 text-right">Sum (KRW)</th><th className="p-3">Memo</th>
                </tr>
              </thead>
              <tbody className="divide-y font-sans">
                {expenses.map(item => (
                  <tr key={item.id} className="font-sans font-sans font-sans font-sans font-sans">
                    <td className="p-3">{item.date}</td><td className="p-3 font-bold text-red-600 uppercase font-sans font-sans font-sans">{item.category.split(' (')[0]}</td>
                    <td className="p-3 text-right font-black font-sans font-sans">₩{item.krwAmount.toLocaleString()}</td><td className="p-3 italic text-slate-500 font-sans font-sans font-sans">{item.description}</td>
                  </tr>
                ))}
              </tbody>
            </table>
            <div className="flex justify-end mt-12 font-sans font-sans font-sans font-sans">
              <div className="bg-slate-900 text-white p-6 rounded-xl text-right min-w-[280px] font-sans">
                <p className="text-[10px] font-bold text-white/40 uppercase tracking-widest mb-1 font-sans">Grand Total Sum</p>
                <p className="text-3xl font-black italic tracking-tighter font-sans font-sans">KRW {totals.krw.toLocaleString()}</p>
              </div>
            </div>
            <button onClick={handlePrintAction} className="mt-20 w-full bg-slate-900 text-white py-5 rounded-2xl font-black uppercase shadow-2xl no-print active:scale-95 transition-all font-sans font-sans">Confirm & Print Report</button>
          </div>
        </div>
      )}

      {/* ➕ 지출 입력 폼 */}
      {showAddForm && (
        <div className="fixed inset-0 z-50 bg-slate-900/60 backdrop-blur-md flex items-center p-4 font-sans font-sans">
          <div className="bg-white w-full max-w-sm mx-auto rounded-[3rem] p-8 animate-in zoom-in-95 shadow-2xl font-sans font-sans font-sans font-sans">
            <div className="flex justify-between items-center mb-6 font-sans">
              <div className="flex items-center gap-2 font-sans font-sans font-sans font-sans font-sans font-sans"><Tag size={18} className="text-red-600 font-sans" /><h3 className="font-black uppercase text-sm font-sans">Add Expense</h3></div>
              <button onClick={() => setShowAddForm(false)} className="p-1 hover:bg-slate-100 rounded-full transition-colors font-sans"><X size={20}/></button>
            </div>
            <form onSubmit={addExpense} className="space-y-4 font-sans font-sans font-sans font-sans font-sans font-sans font-sans font-sans">
              <input type="date" className="w-full p-4 bg-slate-50 rounded-2xl font-bold text-xs font-sans font-sans font-sans" value={formData.date} onChange={e => setFormData({...formData, date: e.target.value})} />
              <div className="grid grid-cols-2 gap-3 font-sans font-sans font-sans font-sans font-sans font-sans font-sans font-sans">
                <select className="p-4 bg-slate-50 rounded-2xl font-bold text-xs font-sans font-sans" value={formData.currency} onChange={e => {
                  const m = currencyList.find(c => c.code === e.target.value);
                  setFormData({...formData, currency: m.code, symbol: m.symbol, rate: m.defaultRate.toString()});
                }}>{currencyList.map(c => <option key={c.code} value={c.code}>{c.label}</option>)}</select>
                <input type="number" className="p-4 bg-red-50 text-red-700 rounded-2xl font-black text-sm text-center font-sans font-sans font-sans" value={formData.rate} onChange={e => setFormData({...formData, rate: e.target.value})} />
              </div>
              <input type="text" list="desc-presets" className="w-full p-4 bg-slate-50 rounded-2xl text-xs font-bold font-sans font-sans font-sans font-sans font-sans font-sans font-sans font-sans" placeholder="Description (e.g. Lunch)" value={formData.description} onChange={e => setFormData({...formData, description: e.target.value})} />
              <datalist id="desc-presets">
                {categoryPresets[formData.category]?.map(p => <option key={p} value={p} />)}
              </datalist>
              <div className="relative font-sans font-sans font-sans font-sans font-sans font-sans font-sans font-sans font-sans font-sans font-sans font-sans font-sans">
                <span className="absolute left-4 top-4 font-black text-slate-400 font-sans font-sans font-sans font-sans font-sans font-sans font-sans font-sans font-sans font-sans">{formData.symbol}</span>
                <input type="number" className="w-full pl-10 p-4 bg-slate-50 rounded-2xl font-black text-xl font-sans font-sans font-sans font-sans font-sans font-sans font-sans font-sans font-sans font-sans font-sans" placeholder="0" value={formData.amount} onChange={e => setFormData({...formData, amount: e.target.value})} />
              </div>
              <button type="submit" className="w-full p-5 bg-slate-900 text-white rounded-[2rem] font-black uppercase active:scale-95 transition-all font-sans font-sans font-sans font-sans font-sans font-sans font-sans font-sans">Save to List</button>
            </form>
          </div>
        </div>
      )}

      {/* 📚 아카이브 모달 */}
      {showArchive && (
        <div className="fixed inset-0 z-50 bg-slate-900/60 backdrop-blur-md flex items-end font-sans">
          <div className="bg-white w-full rounded-t-[3.5rem] p-8 max-h-[90vh] overflow-y-auto animate-in slide-in-from-bottom shadow-2xl font-sans font-sans font-sans font-sans font-sans">
            <div className="flex justify-between items-center mb-8 font-sans font-sans font-sans">
               <button onClick={() => setShowArchive(false)} className="p-2 bg-slate-100 rounded-full transition-colors font-sans"><ArrowLeft size={18} /></button>
               <h3 className="text-xl font-black text-slate-800 tracking-tighter">Project Archive</h3>
               <Archive size={20} className="text-slate-400 font-sans font-sans font-sans font-sans font-sans" />
            </div>
            <button onClick={() => { setTripInfo({...tripInfo, title: ''}); setShowArchive(false); }} className="w-full p-6 bg-slate-50 border-2 border-dashed border-slate-200 rounded-[2.5rem] flex items-center justify-center gap-3 text-slate-900 font-black mb-6 font-sans">
              <FolderPlus size={20} className="font-sans font-sans font-sans font-sans" /> Start New Project
            </button>
            <div className="space-y-4 pb-12 font-sans font-sans font-sans font-sans font-sans font-sans">
              {savedReports.map(r => (
                <div key={r.id} className="p-6 bg-white rounded-[2.5rem] border border-slate-100 space-y-4 shadow-sm font-sans font-sans font-sans font-sans font-sans">
                  <div className="flex justify-between items-start font-sans">
                    <div className="font-sans font-sans font-sans font-sans"><p className="font-black text-slate-800 text-base font-sans">{r.title || "Untitled"}</p><p className="text-[10px] font-bold text-slate-400 uppercase tracking-widest font-sans font-sans font-sans">{r.startDate} • {r.destination}</p></div>
                    <p className="text-lg font-black text-red-600 tracking-tighter font-sans font-sans font-sans font-sans">₩{r.totals?.krw?.toLocaleString() || 0}</p>
                  </div>
                  <div className="flex gap-2 font-sans font-sans font-sans font-sans">
                    <button onClick={() => loadProject(r)} className="flex-1 py-3 bg-slate-50 rounded-2xl text-[10px] font-black text-slate-600 uppercase flex items-center gap-2 active:scale-95 font-sans font-sans">Edit / Load</button>
                    <button onClick={() => deleteDoc(doc(db, 'artifacts', appId, 'users', user.uid, 'finalized_reports', r.id))} className="p-3 bg-slate-50 rounded-2xl text-red-400 active:scale-95 font-sans font-sans"><Trash2 size={14} /></button>
                  </div>
                </div>
              ))}
            </div>
          </div>
        </div>
      )}

      {/* ⚠️ 최종 저장 확인 */}
      {showConfirmModal && (
        <div className="fixed inset-0 z-[110] bg-slate-900/80 backdrop-blur-md flex items-center justify-center p-6 font-sans font-sans font-sans font-sans font-sans font-sans font-sans">
          <div className="bg-white w-full max-w-xs rounded-[2.5rem] p-8 space-y-6 text-center animate-in zoom-in-95 font-sans">
            <div className="mx-auto w-14 h-14 bg-orange-50 text-orange-500 rounded-full flex items-center justify-center font-sans font-sans font-sans font-sans font-sans"><AlertCircle size={28} /></div>
            <div className="space-y-2 font-sans font-sans font-sans font-sans">
              <h4 className="font-black text-slate-800 text-lg">Save & Archive?</h4>
              <p className="text-xs text-slate-400">Current records will be moved to Archive.</p>
            </div>
            {saveStatus === 'success' ? (
              <div className="py-4 text-green-500 font-bold flex flex-col items-center gap-2 animate-in fade-in font-sans font-sans font-sans font-sans"><CheckCircle2 size={48} /><span>Saved!</span></div>
            ) : (
              <div className="flex flex-col gap-2 font-sans font-sans font-sans font-sans font-sans font-sans font-sans">
                <button onClick={finalizeAndReset} className="w-full py-4 bg-slate-900 text-white rounded-2xl font-black text-xs uppercase tracking-widest transition-all active:scale-95 font-sans font-sans font-sans">{saveStatus === 'saving' ? "Saving..." : "Yes, Save & Exit"}</button>
                <button onClick={() => setShowConfirmModal(false)} className="w-full py-4 bg-slate-100 text-slate-400 rounded-2xl font-black text-xs uppercase tracking-widest transition-all active:scale-95 font-sans font-sans font-sans">Cancel</button>
              </div>
            )}
          </div>
        </div>
      )}
    </div>
  );
};

export default App;
