<template>
    <div class="result-form">
        <v-card-title>
            {{ playTable }}番テーブル結果報告
            <v-spacer></v-spacer>
        </v-card-title>
        <v-card-text>
            <v-form ref="test_form">
                <v-radio-group v-model="Result.winnerId"
                :rules="winRules">
                    <v-radio
                    :label='user1Name'
                    :value='user1No'
                    :disabled="success"
                    ></v-radio>
                    <v-radio
                    :label='user2Name'
                    :value='user2No'
                    :disabled="success"
                    ></v-radio>
                    <v-radio
                    :label='`両者敗北`'
                    :value='-1'
                    :disabled="success"
                    ></v-radio>
                </v-radio-group>
                <v-text-field
                    v-model="Result.user1Id"
                    type="number"
                    :label="`${ user1Name }のデュエマID(*)`"
                    :rules="dmidRules"
                    :counter="6"
                    :disabled="success"
                    required
                ></v-text-field>
                <v-text-field
                    v-model="Result.user2Id"
                    type="number"
                    :label="`${ user2Name }のデュエマID(*)`"
                    :rules="dmidRules"
                    :counter="6"
                    :disabled="success"
                    required
                ></v-text-field>
            </v-form>
        </v-card-text>
        <v-card-action>
            <v-btn
                text
                v-on:click="submit"
                color="info"
                :disabled="success"
            >結果報告</v-btn>
            <span v-if="success">勝者：{{ Result.winnerId }}で報告済み。</span>
            <span v-if="success">報告済みのため変更できません。</span>
            
        </v-card-action>
    </div>
</template>

<style scoped>
.Resultbar {
    padding: 0 5%;
    margin: 0 5%;
}
</style>

<script>
import { mapState } from 'vuex';

export default {
    data(){
        return {
            user1No: '111',
            user2No: '999',
            user1Name: '1roTK',
            user2Name: 'ジロウ',
            playTable: '10',
            success: false,
            Result: {
                winnerId: '',
                user1Id: '',
                user2Id: '',
            },
            winRules: [
                v => !!v || '勝者を選択してください'            
            ],
            dmidRules: [
                v => !!v || 'デュエマIDを入力してください',
                v => /^[0-9]*$/.test(v) || '数値で入力してください',
                v => (v.length <= 6) || '6文字で入力してください'
            ],
        };
    },
    
    methods: {
        submit() {
            if (this.$refs.test_form.validate())  {
                if (confirm (this.Result.winnerId + 'の勝利で結果報告します。')) {
                    alert('報告が完了しました。次のラウンドまでお待ちください。')
                    this.success = true;
                }           
            } else {
                this.success = false;
            }
        }

    },    
    computed: {
        ...mapState([
            'players',
        ]),
    },
};
</script>
