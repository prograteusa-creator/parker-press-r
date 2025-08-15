<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>Parker Press — Pro Resumes</title>
<meta name="description" content="ATS-friendly resumes, fast turnaround." />
<meta property="og:title" content="Parker Press — Pro Resumes">
<meta property="og:description" content="ATS-friendly resumes. Pay, submit intake, and get a polished resume fast.">
<meta property="og:type" content="website">
<meta property="og:url" content="https://prograteusa-creator.github.io/parker-press-r/">
<meta name="theme-color" content="#0b84ff">
<style>
  :root { --bg:#0b0b0c; --card:#111114; --muted:#9aa0a6; --text:#f5f7fa; --accent:#00d4ff; }
  *{box-sizing:border-box} body{margin:0;background:var(--bg);color:var(--text);font:16px/1.45 system-ui,-apple-system,Segoe UI,Roboto,Arial}
  .wrap{max-width:980px;margin:28px auto;padding:0 16px}
  h1{font-size:32px;line-height:1.1;margin:0 0 6px;font-weight:800}
  p.lead{margin:0;color:var(--muted)}
  .grid{display:grid;gap:14px}
  @media(min-width:860px){.plans{grid-template-columns:repeat(3,1fr)}}
  .card{background:var(--card);border:1px solid #1d1f22;border-radius:18px;padding:16px}
  .price{font-size:34px;font-weight:900;margin:6px 0}
  .btn{display:inline-flex;gap:8px;align-items:center;justify-content:center;padding:12px 14px;border-radius:12px;border:1px solid #2a2d31;background:#0d0f12;color:#fff;cursor:pointer;text-decoration:none}
  .btn.primary{background:#0b84ff;border-color:#0b84ff}
  .muted{color:var(--muted)}
  .ok{background:#0e4429;border:1px solid #1a7f37;padding:10px;border-radius:12px;margin:10px 0}
  input,textarea{width:100%;padding:10px;border-radius:12px;border:1px solid #2a2d31;background:#0c0e11;color:#fff}
  textarea{min-height:110px}
  .faq-item{border-top:1px solid #1e2125;padding:10px 0}
  .small{font-size:12px}
  .row{display:grid;gap:10px}
  @media(min-width:720px){.row{grid-template-columns:1fr 1fr}}
  .link{color:var(--accent);text-decoration:none}
  .socials a{padding:8px 12px;border-radius:8px;color:#fff;text-decoration:none}
</style>
<script>
  const PAYPAL_CLIENT_ID = "3ztxQd0FVwUF4dPjQ7tb2rwT";
</script>
<script src="https://www.paypal.com/sdk/js?client-id=3ztxQd0FVwUF4dPjQ7tb2rwT&currency=USD" defer></script>
<script>
  document.addEventListener('DOMContentLoaded', () => {
    setupPayPal();
  });

  function setupPayPal(){
    const plans = [
      {name:'Starter', price:49},
      {name:'Pro', price:79},
      {name:'Powerhouse', price:129}
    ];
    for(const p of plans){
      const mount = document.getElementById(`pp-${p.name.toLowerCase()}`);
      if(!mount) continue;
      paypal.Buttons({
        style: { layout:'vertical' },
        createOrder: (_data, actions) => actions.order.create({
          purchase_units: [{ amount: { value: String(p.price) }, description: `${p.name} Resume Plan`}],
        }),
        onApprove: async (_data, actions) => {
          const details = await actions.order.capture();
          const orderId = details?.id || Math.random().toString(36).slice(2,10).toUpperCase();
          successFlow(p.name, orderId);
        }
      }).render(mount);
    }
  }

  function successFlow(plan, orderId){
    const banner = document.getElementById('success');
    banner.innerHTML = `Payment received for <b>${plan}</b>. Order ID: <b>${orderId}</b>. Scroll to intake below.`;
    banner.style.display = 'block';
    document.getElementById('plan').value = plan;
    document.getElementById('order').value = orderId;
    location.hash = 'intake';
  }

  function copyPromo(){
    const url = new URL(location.href);
    url.searchParams.set('utm_source','social');
    url.searchParams.set('utm_medium','organic');
    url.searchParams.set('utm_campaign','resume_launch');
    navigator.clipboard.writeText(`Get a pro, ATS-friendly resume in 24h: ${url}`).then(()=>{
      alert('Promo link copied');
    }).catch(()=>{ alert('Copy failed'); });
  }

  function faqAsk(){
    const q = (document.getElementById('faqq').value||'').toLowerCase().trim();
    const out = document.getElementById('faqa');
    const bank = [
      {k:'turnaround', a:'Typical turnaround is 24–48 hours depending on plan and your intake detail.'},
      {k:'ats', a:'Yes — we use clean structure and job-specific keywords to be ATS-friendly.'},
      {k:'refund', a:'If you’re not happy after the first draft, we’ll revise or refund — your choice.'},
      {k:'cover', a:'Cover letters are included in Pro and Powerhouse.'},
      {k:'linkedin', a:'LinkedIn polish is included in Powerhouse.'}
    ];
    const hit = bank.find(x => q.includes(x.k));
    out.textContent = hit ? hit.a : 'I can help with pricing, turnaround, ATS, refunds, or what each plan includes.';
  }
</script>
</head>
<body>
  <div class="wrap">
    <h1>Parker Press — Pro Resumes</h1>
    <p class="lead">ATS-friendly resumes, fast turnaround. Pay, fill intake, and we start.</p>

    <div id="success" class="ok" style="display:none"></div>

    <section class="grid plans" aria-label="Plans">
      <div class="card">
        <div class="muted small">Starter</div>
        <div class="price">$49</div>
        <div id="pp-starter"></div>
      </div>
      <div class="card">
        <div class="muted small">Pro</div>
        <div class="price">$79</div>
        <div id="pp-pro"></div>
      </div>
      <div class="card">
        <div class="muted small">Powerhouse</div>
        <div class="price">$129</div>
        <div id="pp-powerhouse"></div>
      </div>
    </section>

    <section id="intake" class="card" style="margin-top:16px">
      <h2>Project Intake</h2>
      <form action="https://formspree.io/f/xyyylive" method="POST" class="grid" onsubmit="setTimeout(()=>{alert('Thanks! We’ll follow up by email.');},100)">
        <div class="row">
          <input id="name" name="name" placeholder="Your name" />
          <input id="email" name="email" placeholder="Your email" type="email" required />
        </div>
        <input id="role" name="role" placeholder="Target role" />
        <textarea id="jobs" name="jobs" placeholder="Paste job URLs"></textarea>
        <textarea id="notes" name="notes" placeholder="Notes"></textarea>
        <input type="hidden" id="plan" name="plan" />
        <input type="hidden" id="order" name="order" />
        <button class="btn primary" type="submit">Send Intake</button>
      </form>
    </section>

    <section class="card" style="margin-top:16px">
      <h2>FAQ</h2>
      <input id="faqq" placeholder="Ask a question" onkeydown="if(event.key==='Enter'){event.preventDefault();faqAsk();}"/>
      <button class="btn" style="margin-top:8px" onclick="faqAsk()">Ask</button>
      <div id="faqa" class="small" style="margin-top:8px">I can help with pricing, turnaround, ATS, refunds, and what’s included.</div>
    </section>

    <section class="card" style="margin-top:16px">
      <h2>Share</h2>
      <button class="btn" onclick="copyPromo()">Copy Promo Link</button>
    </section>

    <section class="card" style="margin-top:16px">
      <h2>Follow Us</h2>
      <div class="socials">
        <a style="background:#1877F2" href="https://facebook.com/" target="_blank">Facebook</a>
        <a style="background:#E4405F" href="https://instagram.com/" target="_blank">Instagram</a>
        <a style="background:#000" href="https://tiktok.com/" target="_blank">TikTok</a>
        <a style="background:#0077B5" href="https://linkedin.com/" target="_blank">LinkedIn</a>
        <a style="background:#000" href="https://twitter.com/" target="_blank">X / Twitter</a>
      </div>
    </section>

    <footer class="small muted" style="margin:18px 0 40px">© Parker Press</footer>
  </div>
</body>
</html>
