<script lang="ts">
    import type { UserDonderData } from "$lib/module/common/user/types";
    import { getTheme } from "$lib/module/layout/theme";
    import { getI18N, getLang } from "$lib/module/common/i18n/i18n";
    import { DateTime } from "luxon";

    interface Props {
        donderData: UserDonderData;
        loaded?: boolean;
    }

    let { donderData, loaded = $bindable(false) }: Props = $props();

    const [theme] = getTheme();
    const lang = getLang();
    let i18n = $derived(getI18N("/auth/user/donder", $lang));
</script>

<div class="container">
    <img
        src={donderData.donder.myDon}
        alt={i18n.myDon}
        onload={() => {
            loaded = true;
        }}
        onerror={() => {
            loaded = true;
        }}
    />
    <div class="div-table" data-theme={$theme}>
        <div class="div-tr">
            <div class="div-td taikonumber">
                {donderData.donder.taikoNumber}
            </div>
        </div>
        <div class="div-tr">
            <div class="div-td">
                {donderData.donder.nickname}
            </div>
        </div>
    </div>
    <div class="last-update">
        {i18n.lastUpdate}: {DateTime.fromJSDate(donderData.lastUpdate).toFormat(
            "yyyy-MM-dd HH:mm:ss",
        )}
    </div>
</div>

<style>
    .container {
        display: flex;
        flex-direction: column;
        align-items: center;
        width: 300px;
        max-width: 100%;
        row-gap: 5px;
    }

    .div-table {
        width: 100%;

        border: 1px solid black;
        border-radius: 6px;
    }

    img {
        width: 100%;
        max-width: 200px;
    }

    .div-td {
        text-align: center;
        padding: 0;
        transform: translateY(-2px);
    }
    .div-tr:nth-child(1) .div-td {
        padding-bottom: 1px;
        border-bottom: 1px solid black;
    }

    .div-table[data-theme="dark"],
    .div-table[data-theme="dark"] .div-td {
        border-color: #818181;
    }

    .taikonumber {
        font-size: 13px;
    }

    .last-update {
        font-size: 13px;
    }
</style>
