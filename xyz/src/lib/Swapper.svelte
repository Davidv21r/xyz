<script>
  // UI
  import Button from "./Button.svelte";
  import Token from "./Token.svelte";
  import Amount from "./Amount.svelte";
  import IconSwitch from "./HeroiconsSolidArrowsRightLeft.svelte";
  import IconSwitchVertical from "./HeroiconsSolidArrowsUpDown.svelte";
  import Logo from "./Logo.svelte";
  import Dashboard from "./Dashboard.svelte";
  import Wallet from "./Wallet.svelte";
  import Footer from "./Footer.svelte";

  // STATE
  export let tokenA = "USDT";
  export let tokenB = "XYZ";
  export let ABRate = 2.34567891234567; // exchange rate
  export let platformTokenABalance = 20240311.321; // platform balance (Token A)
  export let myTokenABalance = 12.33; // user balance (Token A)
  export let myTokenBBalance = 2024.0311; // user balance (Token B)

  // SWAP AMOUNT
  let payAmount; // bind user input
  $: getAmount = !isBuy ? payAmount * ABRate : payAmount / ABRate;
  let isBuy = true; // buy or sell

  // WALLET
  let connectedWallet = "Metamask";
  let address = "0x1234567890ABCDEF1234567890ABCDEF12345678";

  // DASHBOARD
  $: dashboard = [
    { name: `$${tokenA}/$${tokenB}`, value: ABRate.toLocaleString("en-US", { maximumFractionDigits: 9 }) },
    {
      name: `$${tokenA} in Platform`,
      value: platformTokenABalance.toLocaleString("en-US", { maximumFractionDigits: 2 }),
    },
  ];

  // FUNCTIONS
  function connectWallet() {
    alert("connect wallet");
    console.log("connect wallet");
  }
  function swap() {
    alert("swap");
    console.log("swap");
  }
</script>

<!-- main -->
<div class="w-full h-full flex flex-col flex-1 self-center p-6 items-center">
  <!-- card -->
  <div
    class="w-fit max-w-full flex flex-col items-stretch bg-stone-950 border-stone-800 border p-6 rounded-3xl gap-4 shadow-lg"
  >
    <Logo txt={tokenB} />
    <Dashboard {dashboard} />
    <!-- swap -->
    <!-- buy & sell [old] -->
    <!-- <div class="flex gap-4 relative justify-stretch">
        <Token class="flex-1" tokenName={isBuy ? tokenA : tokenB}></Token>
        <Token class="flex-1" method="To" tokenName={isBuy ? tokenB : tokenA}></Token>
        <button
        on:click={() => (isBuy = !isBuy)}
        class="absolute top-[50%] left-[50%] translate-x-[-50%] translate-y-[-50%] rounded-full flex items-center justify-center w-10 h-10 bg-lime-500 text-lime-50 border border-lime-400 hover:bg-lime-400 font-semibold shadow-lg transition-all duration-300 ease-in-out hover:shadow-lime-500/30"
        >
        <IconSwitch />
      </button>
    </div> -->
    <!-- buy & sell start -->
    <div class="flex flex-col items-stretch gap-2">
      <h2 class="font-bold text-lg">Swap</h2>
      <Amount
        on:setMax={() => (payAmount = isBuy ? myTokenABalance : myTokenBBalance)}
        max={isBuy ? myTokenABalance : myTokenBBalance}
        title={"You " + (isBuy ? "Pay" : "Sell") + " $" + (isBuy ? tokenA : tokenB)}
        bind:value={payAmount}
        caption={"Available: " + (isBuy ? myTokenABalance : myTokenBBalance)}
      />
      <!-- switch button -->
      <div class="relative">
        <button
          on:click={() => (isBuy = !isBuy)}
          class="-my-5 mx-auto rounded-full flex items-center justify-center w-10 h-10 bg-lime-500 text-lime-50 border border-lime-400 hover:bg-lime-400 font-semibold shadow-lg transition-all duration-300 ease-in-out hover:shadow-lime-500/30"
        >
          <IconSwitchVertical />
        </button>
      </div>
      <Amount readonly title={"You Get $" + (isBuy ? tokenB : tokenA)} bind:value={getAmount} />
    </div>
    {#if !connectedWallet}
      <Button>Connect Wallet</Button>
    {:else}
      <Button>Swap</Button>
      <Wallet {connectedWallet} {address} />
    {/if}
    <!-- buy & sell end -->
  </div>
  <Footer />
</div>
