import React, { useState, useRef, useEffect } from 'react';

const masks = {
  pink: '/mask-pink.png', // アップロードいただいた画像パス
  white: '/mask-white.png',
  blue: '/mask-blue.png'
};

export default function BriefsDanDogApp() {
  const [color, setColor] = useState('pink');
  const [initial, setInitial] = useState('C');
  const [name, setName] = useState('');
  const [photo, setPhoto] = useState(null);
  const canvasRef = useRef(null);

  // キャンバスに描画する関数
  const drawCard = () => {
    const canvas = canvasRef.current;
    const ctx = canvas.getContext('2d');
    // ここで背景、写真、マスク、イニシャルを重ね合わせる処理を実装
    // 実際には画像読み込み後に描画するようにuseEffect等で制御します
  };

  return (
    <div className="bg-[#1a1a1a] text-white min-h-screen p-6 font-sans">
      <header className="text-center mb-8">
        <h1 className="text-3xl font-bold tracking-widest text-transparent bg-clip-text bg-gradient-to-r from-yellow-500 to-yellow-200">
          BRIEFSDAN-DOG
        </h1>
        <p className="text-gray-400 uppercase text-sm tracking-[0.2em]">VIP DOG CARD</p>
      </header>

      {/* プレビューエリア */}
      <div className="border border-yellow-600 rounded-lg p-2 bg-black shadow-[0_0_20px_rgba(202,138,4,0.3)] mb-8">
        <canvas ref={canvasRef} width={400} height={400} className="w-full h-auto bg-gray-900 rounded" />
      </div>

      {/* コントロールパネル */}
      <div className="space-y-6">
        <div>
          <label className="text-yellow-600 block mb-2 font-bold">MASK COLOR</label>
          <div className="flex gap-4">
            {Object.keys(masks).map((c) => (
              <button 
                key={c} 
                onClick={() => setColor(c)}
                className={`w-12 h-12 rounded-full border-2 ${color === c ? 'border-white' : 'border-transparent'}`}
                style={{ backgroundColor: c === 'pink' ? '#ec4899' : c === 'white' ? '#f3f4f6' : '#3b82f6' }}
              />
            ))}
          </div>
        </div>

        <input 
          type="text" 
          maxLength={1} 
          placeholder="INITIAL" 
          className="w-full bg-[#2a2a2a] p-4 rounded border border-gray-700 text-center"
          onChange={(e) => setInitial(e.target.value.toUpperCase())}
        />
        
        <button className="w-full bg-yellow-600 py-4 rounded font-bold text-black hover:bg-yellow-500 transition">
          CREATE CARD
        </button>
      </div>
    </div>
  );
}
// 追加: 写真アップロード処理
const handleImageUpload = (e) => {
  const file = e.target.files[0];
  const reader = new FileReader();
  reader.onload = (event) => {
    setPhoto(event.target.result); // 読み込んだ画像をセット
  };
  reader.readAsDataURL(file);
};

// Returnの中にこれを追加
<input type="file" onChange={handleImageUpload} className="text-white" />
{photo && <img src={photo} alt="Preview" className="w-full h-auto" />}
