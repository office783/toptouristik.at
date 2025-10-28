import React, { useEffect, useState } from "react";
return (
<div className="grid lg:grid-cols-3 gap-8">
<div className="lg:col-span-2 bg-white rounded-2xl border border-slate-200 p-6">
<h3 className="text-xl font-semibold">Buchung abschließen</h3>
<div className="mt-4 grid sm:grid-cols-2 gap-4">
<Field label="Reiseziel" value={`${selected.destination}`} />
<Field label="Reise" value={`${selected.title} (${selected.nights} Nächte)`} />
<Field label="Anreise" value={query.start || "—"} />
<Field label="Abreise" value={query.end || "—"} />
<Field label="Gäste" value={String(query.guests)} />
<Field label="Gesamt" value={formatCents(total)} />
</div>
<div className="mt-6 text-sm text-slate-600">Mit der Buchung akzeptieren Sie unsere AGB und Datenschutzbestimmungen.</div>
<div className="mt-6 flex gap-3">
<button onClick={onBack} className="rounded-xl border border-slate-300 px-4 py-2">Zurück</button>
<button disabled={loading} onClick={onPay} className="rounded-xl bg-slate-900 text-white px-4 py-2 disabled:opacity-60">{loading ? "Wird verarbeitet…" : "Jetzt bezahlen"}</button>
</div>
</div>
<div className="bg-white rounded-2xl border border-slate-200 overflow-hidden">
<img src={selected.img} alt="Ausgewähltes Paket" className="w-full h-40 object-cover" />
<div className="p-5 text-sm text-slate-700">
<div className="font-medium">Inklusive</div>
<ul className="mt-2 space-y-1">
{selected.highlights.map((h, i) => <li key={i} className="flex items-center gap-2"><Dot/>{h}</li>)}
</ul>
</div>
</div>
</div>
);
}


function Field({ label, value }: { label: string; value: string }) {
return (
<div>
<div className="text-xs uppercase tracking-wide text-slate-500">{label}</div>
<div className="mt-1 font-medium">{value}</div>
</div>
);
}


function Benefit({ title, desc, children }: { title: string; desc: string; children: React.ReactNode }) {
return (
<div className="bg-white rounded-2xl border border-slate-200 p-6">
<div className="h-10 w-10 rounded-xl bg-slate-900 text-white flex items-center justify-center">{children}</div>
<div className="mt-3 font-semibold">{title}</div>
<div className="text-slate-600 text-sm mt-1">{desc}</div>
</div>
);
}


// === Icons (simple SVGs, no externals) ===
function Dot() {
return (
<svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor" className="text-slate-400">
<circle cx="12" cy="12" r="4" />
</svg>
);
}
function Shield() {
return (
<svg viewBox="0 0 24 24" className="w-5 h-5" fill="currentColor"><path d="M12 2l7 4v6c0 5-3.4 9.7-7 10-3.6-.3-7-5-7-10V6l7-4z"/></svg>
);
}
function Tag() {
return (
<svg viewBox="0 0 24 24" className="w-5 h-5" fill="currentColor"><path d="M10 3l9 9-7 7-9-9V3h7zm0 2H6v4l7 7 5-5-8-8z"/></svg>
);
}
function Headphones() {
return (
<svg viewBox="0 0 24 24" className="w-5 h-5" fill="currentColor"><path d="M12 3a9 9 0 00-9 9v6a3 3 0 003 3h1v-8H6a7 7 0 0114 0h-1v8h1a3 3 0 003-3v-6a9 9 0 00-9-9z"/></svg>
);
}


// === Utils ===
function formatCents(cents: number) {
return new Intl.NumberFormat("de-AT", { style: "currency", currency: "EUR" }).format(cents / 100);
}
