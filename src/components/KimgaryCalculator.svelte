<script>
  let items = [""];
  $: subTotal = items.reduce((acc, amt) => acc + Number(amt), 0);
  $: discountedAmt = subTotal * 0.75;
  $: gst = discountedAmt * 0.06;
  $: serviceCharge = subTotal * 0.1;
  $: total = (discountedAmt + gst + serviceCharge).toFixed(2);

  /** @param {MouseEvent} event */
  function addRowHandler(event) {
    items.push("");
    items = items;
    console.log(items);
  }
</script>

<table class="table-auto border-collapse border border-slate-300 w-full">
  <thead class="font-bold">
    <th class="border border-slate-300 py-2">No.</th>
    <th class="border border-slate-300 py-2">Amount</th>
  </thead>
  <tbody>
    {#each items as item, index}
      <tr>
        <td class="border border-slate-300 w-12 text-center">
          {index + 1}
        </td>
        <td class="border border-slate-300 text-xl md:text-2xl">
          <div class="flex items-center">
            <span class="px-4 font-semibold">RM</span>
            <input
              class="w-full py-2 px-4 border border-amber-500"
              autofocus
              type="number"
              name={"amount" + index}
              id={"amount" + index}
              bind:value={item}
            />
          </div>
        </td>
      </tr>
    {/each}
  </tbody>
  <tfoot>
    <tr>
      <td class="py-2 px-4" colspan="2">
        <button
          on:click={addRowHandler}
          class="bg-sky-600 rounded-sm border border-sky-950 py-2 px-4 flex gap-2 ml-auto hover:bg-sky-500 active:bg-sky-700 text-white"
        >
          <svg
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            view-box="0 0 24 24"
            stroke-width={1.5}
            stroke="currentColor"
            class="w-6 h-6"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              d="M12 4.5v15m7.5-7.5h-15"
            />
          </svg>
          Add more items
        </button>
      </td>
    </tr>
  </tfoot>
</table>

<h1 class="text-7xl md:text-9xl text-sky-600 w-full text-center mt-4">
  RM {total}
</h1>

<table
  class="table-auto w-full bg-white border-collapse border border-slate-300 mt-8"
>
  <thead>
    <tr>
      <th class="text-3xl text-center py-2" colspan="2">
        Calculation Breakdown
      </th>
    </tr>
  </thead>
  <tbody>
    <tr class="border border-slate-300">
      <td class="p-4">
        <p class="text-xl md:text-2xl">Sub Total:</p>
      </td>
      <td class="text-xl md:text-2xl p-4 text-right whitespace-nowrap">
        RM {subTotal.toFixed(2)}
      </td>
    </tr>

    <tr class="border border-slate-300">
      <td class="p-4">
        <p class="text-xl md:text-2xl">Discounted Amount (25%):</p>
        <span class="text-base">(Sub Total x 0.75)</span>
      </td>
      <td class="text-xl md:text-2xl p-4 text-right whitespace-nowrap">
        RM {discountedAmt.toFixed(2)}
      </td>
    </tr>

    <tr class="border border-slate-300">
      <td class="p-4">
        <p class="text-xl md:text-2xl">GST (6%):</p>
        <span class="text-base">(Discounted Amount x 0.06)</span>
      </td>
      <td class="text-xl md:text-2xl p-4 text-right whitespace-nowrap">
        RM {gst.toFixed(2)}
      </td>
    </tr>

    <tr class="border border-slate-300">
      <td class="p-4">
        <p class="text-xl md:text-2xl">Service Charge (10%):</p>
        <span class="text-base">(Sub Total x 0.10)</span>
      </td>
      <td class="text-xl md:text-2xl p-4 text-right whitespace-nowrap">
        RM {serviceCharge.toFixed(2)}
      </td>
    </tr>

    <tr class="border border-slate-300">
      <td class="p-4">
        <p class="text-xl md:text-2xl">Total:</p>
        <span class="text-base">(Discounted Amount + GST + Service Charge)</span
        >
      </td>
      <td class="text-xl md:text-2xl p-4 text-right whitespace-nowrap">
        RM {total}
      </td>
    </tr>
  </tbody>
</table>
