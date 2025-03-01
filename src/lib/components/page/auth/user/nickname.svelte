<script lang="ts" context="module">
    import { replaceState } from "$app/navigation";

    async function changeNickname(newNickname: string, user: Writable<Record<string, any>>) {
        const result = await userRequestor.changeNickname({ newNickname });
        user.update((v) => {
            v.nickname = newNickname;
            return v;
        })
        return result;
    }
</script>

<script lang="ts">
    import { getContext } from "svelte";
    import { get, type Writable } from "svelte/store";
    import { page } from "$app/stores";
    import { getTheme } from "$lib/module/layout/theme";
    import { userRequestor } from "$lib/module/common/user/user.client";
    import { getI18N, getLang } from "$lib/module/common/i18n/i18n";

    const user = getContext("user") as Writable<{
        provider: string;
        nickname: string;
    }>;

    let nickname = $user.nickname;

    let nicknameFormatError = false;
    $: nicknameFormatError = !/^([a-zA-Z가-힣0-9\-]*)$/.test(nickname);

    let error = "";

    const [theme] = getTheme();
    const lang = getLang();
    $: i18n = getI18N("/auth/user", $lang);
</script>

<div class="div-tr">
    <div class="div-td">{i18n.nickname}</div>
    <div class="div-td">
        <div class="explanation">
            {i18n.nickRule}
        </div>
        <div class="container">
            <div>
                <input
                    bind:value={nickname}
                    class:error={nicknameFormatError}
                />
                <button
                    on:click={() => {
                        error = "";
                        if (nicknameFormatError) {
                            error =
                                i18n.error[
                                    "New nickname is not in the correct format"
                                ];
                        } else {
                            changeNickname(nickname, user).then((result) => {
                                if (result.status === "success") {
                                    alert(i18n.nickChangeSuccess);
                                } else {
                                    error =
                                        i18n.error[result.reason ?? ""] ||
                                        result.reason;
                                }
                            });
                        }
                    }}
                    data-theme={$theme}
                >
                    {i18n.change}
                </button>
            </div>
            {#if error}
                <div style="color:red;">{error}</div>
            {/if}
        </div>
    </div>
</div>

<style>
    .error {
        border: 1px solid red;
        outline: 1px solid red;

        box-sizing: border-box;
    }

    .explanation {
        font-size: 12px;
        color: gray;
    }

    .container {
        width: 100%;
        display: flex;
        flex-direction: row;
        column-gap: 10px;
    }

    @media only screen and (max-width: 1000px) {
        .container {
            flex-direction: column;
        }
    }

    button {
        border: 1px solid #cf4844;
        outline: 0;
        color: black;

        border-radius: 5px;

        height: 22px;

        cursor: pointer;
    }
    button[data-theme="dark"] {
        background-color: black;
        color: white;

        box-sizing: border-box;
        border-color: rgb(145, 145, 145);
    }
</style>
