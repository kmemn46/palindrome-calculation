<template>
  <v-container>
    <v-row class="text-center">
      <v-col class="mb-4">
        <v-card class="mx-auto">
          <v-card-subtitle class="text-left">
            制限：整数10桁までを計算対象としています。
          </v-card-subtitle>
          <v-form ref="form" v-model="valid" lazy-validation>
            <v-container fluid style="background-color: #E8F5E9">
              <v-row dense>
                <v-col cols-6>
                  <v-card>
                    <v-container>
                      <v-row>
                        <v-col cols-12>
                          <v-text-field
                            v-model="input"
                            :counter="10"
                            :rules="inputRules"
                            label="Input"
                            required
                          ></v-text-field>
                        </v-col>
                      </v-row>
                      <v-row>
                        <v-col>
                          <v-btn color="primary" @click="onsubmit">計算</v-btn>
                        </v-col>
                      </v-row>
                    </v-container>
                  </v-card>
                </v-col>
              </v-row>
              <v-row dense>
                <v-col cols-6>
                  <v-card class="mx-auto">
                    <v-card-title class="green--text">
                      <div class="text-h5">
                        計算結果
                      </div>
                    </v-card-title>
                    <v-card-text class="text-center">
                      <div class="text-h3">
                        {{ result }}
                      </div>
                    </v-card-text>
                  </v-card>
                </v-col>
              </v-row>
            </v-container>
          </v-form>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
  export default {
    name: 'Culculation',

    data: () => ({
      result: 0,
      valid: false,
      input: '',
      inputRules: [
        v => !!v || 'Input is required',
        v => v.length <= 10 || 'Input must be less than 10 characters',
        v => isNaN(v) == false || 'Input must be number',
        v => v != 1 || 'Input must not be 1',
      ],
    }),
    methods: {
      onsubmit() {
        // 入力値の検証を実行
        if (this.$refs.form.validate()) {
          this.calculate();
        }
      },
      // ここから回分数の計算
      calculate() {
        var input_num = parseInt(this.input, 10).toString(10) // 前0対応
        var max_int = Number.MAX_SAFE_INTEGER  // JSで安全に扱える整数のMAX
        for (;;) {
          try {
            
            let rev = Array.from(input_num).reverse().join('')
            let rev_int = parseInt(rev, 10)
            let input_num_int = parseInt(input_num, 10)
            
            if (input_num_int == rev_int) {
              this.result = rev_int
              break;
            } else {
              input_num_int += rev_int
              if (input_num_int < max_int) {
                input_num = input_num_int.toString(10)
              } else {
                // 結果がMAXを超えた場合は処理終了
                this.result = 'この数値は計算できません。'
                break;
              }
            }
          } catch(error) {
            console.log("エラー内容：" + error);
            break;
          }
        }
      },
    }
  }
</script>
