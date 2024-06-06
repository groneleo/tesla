<script>
    import { PUBLIC_BASE_URL } from '$env/static/public';
    import axios from "axios";
    import { onMount } from "svelte";

    let prediction = "";
    let errorMessage = "";
    let loading = false;

    let volume = "114289900";
    let industrial_prod = "100.546270";
    let trade_balance = "-54287.955185";
    let unepmloyment_rate = "4.749868";
    let customer_price_idx = "262.028310";
    let fed_eff_rate = "1.428032";
    let prev_close = "103.558682"; 
    let daily_return = "-0.054575";
    let moving_average_10 = "103.929859";
    let moving_average_50 = "105.471389";
    let volatility_10 = "3.161051";
    let bollinger_high = "117.952463";
    let bollinger_low = "90.681138";
    let atr = "6.260700";
    let cci = "-9.834113";
    let momentum = "-0.343225";
    let williams_r = "-52.971498";

    async function handleSubmit() {

        errorMessage = "";
        prediction = "";
        loading = true;

        try {
            const response = await axios.post(PUBLIC_BASE_URL + '/predict', {
                volume: volume,
                industrial_prod: industrial_prod,
                trade_balance: trade_balance,
                unepmloyment_rate: unepmloyment_rate,
                customer_price_idx: customer_price_idx,
                fed_eff_rate: fed_eff_rate,
                prev_close: prev_close,
                daily_return: daily_return,
                moving_average_10: moving_average_10,
                moving_average_50: moving_average_50,
                volatility_10: volatility_10,
                bollinger_high: bollinger_high,
                bollinger_low: bollinger_low,
                atr: atr,
                cci: cci,
                momentum: momentum,
                williams_r: williams_r
            });
            prediction = response.data.prediction;
        } catch (error) {
            errorMessage = "An error occurred while fetching the prediction.";
        } finally {
            loading = false;
        }
    }
</script>

<div class="container">
    <h1>Tesla Stock Price Prediction</h1>
    <form on:submit|preventDefault={handleSubmit}>
        <div class="input-field">
            <label for="volume">Volume:</label>
            <input type="number" step="any" bind:value={volume} required>
        </div>
        <div class="input-field">
            <label for="industrial_prod">Industrial Production:</label>
            <input type="number" step="any" bind:value={industrial_prod} required>
        </div>
        <div class="input-field">
            <label for="trade_balance">Trade Balance:</label>
            <input type="number" step="any" bind:value={trade_balance} required>
        </div>
        <div class="input-field">
            <label for="unepmloyment_rate">Unemployment Rate:</label>
            <input type="number" step="any" bind:value={unepmloyment_rate} required>
        </div>
        <div class="input-field">
            <label for="customer_price_idx">Customer Price Index:</label>
            <input type="number" step="any" bind:value={customer_price_idx} required>
        </div>
        <div class="input-field">
            <label for="fed_eff_rate">Federal Effective Rate:</label>
            <input type="number" step="any" bind:value={fed_eff_rate} required>
        </div>
        <div class="input-field">
            <label for="prev_close">Previous Close:</label>
            <input type="number" step="any" bind:value={prev_close} required>
        </div>
        <div class="input-field">
            <label for="daily_return">Daily Return:</label>
            <input type="number" step="any" bind:value={daily_return} required>
        </div>
        <div class="input-field">
            <label for="moving_average_10">10-day Moving Average:</label>
            <input type="number" step="any" bind:value={moving_average_10} required>
        </div>
        <div class="input-field">
            <label for="moving_average_50">50-day Moving Average:</label>
            <input type="number" step="any" bind:value={moving_average_50} required>
        </div>
        <div class="input-field">
            <label for="volatility_10">10-day Volatility:</label>
            <input type="number" step="any" bind:value={volatility_10} required>
        </div>
        <div class="input-field">
            <label for="bollinger_high">Bollinger High:</label>
            <input type="number" step="any" bind:value={bollinger_high} required>
        </div>
        <div class="input-field">
            <label for="bollinger_low">Bollinger Low:</label>
            <input type="number" step="any" bind:value={bollinger_low} required>
        </div>
        <div class="input-field">
            <label for="atr">Average True Range (ATR):</label>
            <input type="number" step="any" bind:value={atr} required>
        </div>
        <div class="input-field">
            <label for="cci">Commodity Channel Index (CCI):</label>
            <input type="number" step="any" bind:value={cci} required>
        </div>
        <div class="input-field">
            <label for="momentum">Momentum:</label>
            <input type="number" step="any" bind:value={momentum} required>
        </div>
        <div class="input-field">
            <label for="williams_r">Williams %R:</label>
            <input type="number" step="any" bind:value={williams_r} required>
        </div>
        <button type="submit">Predict Stock Price</button>
        {#if errorMessage}
            <div id="error-message" style="color: red; margin-top: 20px;">{errorMessage}</div>
        {/if}
        {#if loading}
            <div class="loading">Loading...</div>
        {:else if prediction}
            <div class="result">
                <h2>Prediction: {prediction}</h2>
            </div>
        {/if}
    </form>
</div>

<style>
    .loading {
        margin-top: 20px;
        font-size: 16px;
        font-weight: bold;
    }
    .input-field {
        margin-bottom: 20px;
    }
    .input-field label {
        display: block;
        margin-bottom: 5px;
    }
    .input-field input {
        width: 100%;
        padding: 8px;
        box-sizing: border-box;
    }
</style>


<!-- <script>
    import { PUBLIC_BASE_URL } from '$env/static/public';
    import axios from "axios";
    import { onMount } from "svelte";

    let prediction = "";
    let errorMessage = "";
    let loading = false;

    // Initial values for input fields
    let open = "";
    let volume = "";
    let industrial_prod = "";
    let trade_balance = "";
    let unemployment_rate = "";
    let customer_price_idx = "";
    let fed_eff_rate = "";
    let daily_return = "";
    let moving_average_5 = "";
    let moving_average_10 = "";
    let volatility_5 = "";

    async function handleSubmit() {

        errorMessage = "";
        prediction = "";
        loading = true;

        try {
            const response = await axios.post(PUBLIC_BASE_URL + '/predict', {
                open: open,
                volume: volume,
                industrial_prod: industrial_prod,
                trade_balance: trade_balance,
                unemployment_rate: unemployment_rate,
                customer_price_idx: customer_price_idx,
                fed_eff_rate: fed_eff_rate,
                daily_return: daily_return,
                moving_average_5: moving_average_5,
                moving_average_10: moving_average_10,
                volatility_5: volatility_5
            });
            prediction = response.data.prediction;
        } catch (error) {
            errorMessage = "An error occurred while fetching the prediction.";
        } finally {
            loading = false;
        }
    }
</script>

<div class="container">
    <h1>Tesla Stock Price Prediction</h1>
    <form on:submit|preventDefault={handleSubmit}>
        <div class="input-field">
            <label for="open">Open Price:</label>
            <input type="number" step="any" bind:value={open} required>
        </div>
        <div class="input-field">
            <label for="volume">Volume:</label>
            <input type="number" step="any" bind:value={volume} required>
        </div>
        <div class="input-field">
            <label for="industrial_prod">Industrial Production:</label>
            <input type="number" step="any" bind:value={industrial_prod} required>
        </div>
        <div class="input-field">
            <label for="trade_balance">Trade Balance:</label>
            <input type="number" step="any" bind:value={trade_balance} required>
        </div>
        <div class="input-field">
            <label for="unemployment_rate">Unemployment Rate:</label>
            <input type="number" step="any" bind:value={unemployment_rate} required>
        </div>
        <div class="input-field">
            <label for="customer_price_idx">Customer Price Index:</label>
            <input type="number" step="any" bind:value={customer_price_idx} required>
        </div>
        <div class="input-field">
            <label for="fed_eff_rate">Federal Effective Rate:</label>
            <input type="number" step="any" bind:value={fed_eff_rate} required>
        </div>
        <div class="input-field">
            <label for="daily_return">Daily Return:</label>
            <input type="number" step="any" bind:value={daily_return} required>
        </div>
        <div class="input-field">
            <label for="moving_average_5">5-day Moving Average:</label>
            <input type="number" step="any" bind:value={moving_average_5} required>
        </div>
        <div class="input-field">
            <label for="moving_average_10">10-day Moving Average:</label>
            <input type="number" step="any" bind:value={moving_average_10} required>
        </div>
        <div class="input-field">
            <label for="volatility_5">5-day Volatility:</label>
            <input type="number" step="any" bind:value={volatility_5} required>
        </div>
        <button type="submit">Predict Stock Price</button>
        {#if errorMessage}
            <div id="error-message" style="color: red; margin-top: 20px;">{errorMessage}</div>
        {/if}
        {#if loading}
            <div class="loading">Loading...</div>
        {:else if prediction}
            <div class="result">
                <h2>Prediction: {prediction}</h2>
            </div>
        {/if}
    </form>
</div>

<style>
    .loading {
        margin-top: 20px;
        font-size: 16px;
        font-weight: bold;
    }
    .input-field {
        margin-bottom: 20px;
    }
    .input-field label {
        display: block;
        margin-bottom: 5px;
    }
    .input-field input {
        width: 100%;
        padding: 8px;
        box-sizing: border-box;
    }
</style> -->
