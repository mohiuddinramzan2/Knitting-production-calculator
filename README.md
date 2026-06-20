# সার্কুলার নিটিং প্রোডাকশন কাউন্টার ক্যালকুলেটর

ছোট, ডিপেন্ডেন্সি-মুক্ত (no build step) ওয়েব অ্যাপ — Single Jersey, Terry ও Fleece ফেব্রিকের জন্য মেশিন কাউন্টার বের করে। পুরো অ্যাপ একটাই ফাইলে: `index.html` (HTML + CSS + JS)।

## ব্যবহার
ব্রাউজারে `index.html` খুলুন। ইনপুট দিলে ফলাফল লাইভ আপডেট হয়; "কাউন্টার বের করো" বাটনে চাপলে রিজাল্ট কার্ডে স্ক্রল করে নিয়ে যাবে।

## GitHub Pages-এ ডিপ্লয়
1. একটা নতুন রিপোজিটরি বানান এবং `index.html` রুটে আপলোড করুন (এই README সহ)।
2. রিপোর **Settings → Pages** এ যান।
3. **Branch** এ `main` (বা `master`) সিলেক্ট করে, ফোল্ডার `/ (root)` রেখে **Save** করুন।
4. কিছুক্ষণ পর `https://<username>.github.io/<repo-name>/` লিংকে অ্যাপ লাইভ হয়ে যাবে।

## ফরমুলাগুলো

**নিডেল সংখ্যা (সব ফেব্রিকের জন্য, অটো-ক্যালকুলেটেড):**
```
needles = 3.14 × needle_gauge × machine_dia
```

**ফিটার (অটো, মিস ফিটার বিয়োগ করার সুযোগ আছে):**
```
fitter_auto   = (machine_dia × 3) + 6
usable_fitter = fitter_auto − miss_fitter_count   (সর্বনিম্ন 1)
```

**Single Jersey:**
```
counters = (kg × 16,936,517 × yarn_count) ÷ stitch_length ÷ needles ÷ usable_fitter
```

**Terry:**
```
yarn_factor = (5314.9 ÷ lycra_denier) − yarn_count
stitch_sum  = poly_stitch_length_1 + poly_stitch_length_2
counters    = (kg × 8,533,792 × yarn_factor) ÷ stitch_sum ÷ needles ÷ usable_fitter
```

**Fleece:**
```
yarn_factor = polyester_count + loop_yarn_count + knit_yarn_count
counters    = (kg × 11,251,982.42 × yarn_factor) ÷ stitch_length ÷ needles ÷ usable_fitter
```

সবগুলো ফরমুলা মূল উদাহরণের সংখ্যা দিয়ে যাচাই করা হয়েছে:
- SJ: 20kg → ≈675.91 কাউন্টার
- Terry: 28kg → ≈2250 কাউন্টার
- Fleece: 34.88kg → ≈2949.10 কাউন্টার

## ফাইল গঠন
```
.
├── index.html      # পুরো অ্যাপ (UI + লজিক)
├── manifest.json   # PWA ম্যানিফেস্ট (অ্যাপের নাম, আইকন, থিম কালার)
├── sw.js           # সার্ভিস ওয়ার্কার (অফলাইন ক্যাশিং)
├── icon-192.png    # অ্যাপ আইকন (ছোট)
├── icon-512.png    # অ্যাপ আইকন (বড়)
└── README.md
```

## Termux দিয়ে APK বানানো (Bubblewrap)
আগে উপরের GitHub Pages ডিপ্লয় শেষ করুন, যাতে আপনার manifest.json একটা লাইভ লিংকে থাকে, যেমন:
`https://<username>.github.io/<repo-name>/manifest.json`

তারপর Termux-এ ধাপে ধাপে কমান্ড চালান — বিস্তারিত নিচের চ্যাটে দেওয়া আছে।

