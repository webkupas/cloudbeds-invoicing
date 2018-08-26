<template>
  <v-app id="inspire">
    <v-form v-model="valid">
      <v-container grid-list-xl>
        <v-layout row justify-space-between>
          <v-flex xs6>
            <v-card>
              <v-card-title primary-title>
                <div>
                  <h3 class="headline mb-0">Contact Info</h3>
                </div>
              </v-card-title>
              <v-card-text>
                  <v-text-field
                    v-model="name"
                    label="Contact Name"
                    required
                  ></v-text-field>
                  <v-text-field
                    v-model="street"
                    label="Street Address"
                    required
                  ></v-text-field>
                  <v-layout row justify-space-between>
                    <v-flex xs5>
                      <v-text-field
                        v-model="city"
                        label="City"
                        required
                      ></v-text-field>
                    </v-flex>
                    <v-flex xs2>
                      <v-text-field
                        v-model="zip"
                        label="Zip"
                        required
                      ></v-text-field>
                    </v-flex>
                    <v-flex xs5>
                      <v-text-field
                        v-model="country"
                        label="Country"
                        required
                      ></v-text-field>
                    </v-flex>
                  </v-layout >
              </v-card-text>

            </v-card>
          </v-flex>

          <v-flex xs6>
            <v-card>
              <v-card-title primary-title>
                <div>
                  <h3 class="headline mb-0">Invoice Info</h3>
                </div>
              </v-card-title>
              <v-card-text>
                <v-layout row justify-space-between>
                  <v-flex xs6>
                    <v-menu
                      ref="menu"
                      :close-on-content-click="false"
                      v-model="menu"
                      :nudge-right="40"
                      :return-value.sync="invoiceDate"
                      lazy
                      transition="scale-transition"
                      offset-y
                      full-width
                      min-width="290px"
                    >
                      <v-text-field
                        slot="activator"
                        v-model="invoiceDate"
                        label="Invoice Date"
                        readonly
                        required
                      ></v-text-field>
                      <v-date-picker v-model="invoiceDate" @input="$refs.menu.save(invoiceDate)" type="month"></v-date-picker>
                    </v-menu>
                  </v-flex>
                  <v-flex xs6>
                    <v-text-field
                      :value="invoiceID"
                      label="Invoice ID"
                      disabled
                    ></v-text-field>
                  </v-flex>
                </v-layout>
                <v-text-field
                    v-model="project"
                    label="Project/Work"
                    required
                  ></v-text-field>
                <v-text-field
                    v-model="department"
                    label="Choose Your Dapartment"
                    required
                  ></v-text-field>
              </v-card-text>
            </v-card>
          </v-flex>
        </v-layout>
        
        <v-layout row>
          <v-flex xs12>
            <v-card>
              <v-card-title primary-title>
                <div>
                  <h3 class="headline mb-0">Description of Work</h3>
                </div>
              </v-card-title>
              <v-card-text>
              <v-toolbar color="white" flat>
                <v-toolbar-title style="width: 50px;">No.</v-toolbar-title>
                <v-toolbar-title>Work description</v-toolbar-title>
                <v-toolbar-title style="width: 100px; margin: 0 15px; text-align: left">Price</v-toolbar-title>
              </v-toolbar>
              <v-divider></v-divider>
              <draggable v-model="rows" element="v-list">

                <v-list-tile
                  v-for="(row, index) in rows"
                    :key="index"
                >
                <div
                class="subheading"
                style="width: 40px; margin-right: 10px"
                disabled
                >{{index+1}}</div>
                  <v-text-field
                  v-model="row.description"
                ></v-text-field>

                  <v-text-field
                  style="width: 100px; margin: 0 15px"
                  v-model="row.price"
                ></v-text-field>

                  <v-list-tile-action>
                    <v-btn flat small fab @click.prevent="removeRow(index)">
                      <v-icon dark color="red">delete_forever</v-icon>
                    </v-btn>
                  </v-list-tile-action>
                </v-list-tile>

              </draggable>
              <v-divider></v-divider>

                <table class="table table-hover">
                  <thead>
                    <tr>
                      <th style="width: 20px;">No.</th>
                      <th>Description</th>
                      <th style="width: 130px;" class="text-right">Price</th>
                      <th style="width: 100px;"></th>
                    </tr>
                  </thead>
                  <draggable v-model="rows" element="tbody">
                    <tr v-for="(row, index) in rows" :key="index">
                      <td> {{ index +1 }} </td>
                      <td>
                        <v-text-field
                        solo
                        v-model="row.description"
                      ></v-text-field>
                      </td>
                      <td>
                       <v-text-field
                        solo
                        v-model="row.price"
                      ></v-text-field>
                      </td>
                      <td>
                        <v-btn flat small fab @click.prevent="removeRow(index)">
                          <v-icon dark color="red">delete_forever</v-icon>
                        </v-btn>
                      </td>
                    </tr>

                    <v-btn color="primary" dark slot="footer" @click.prevent="addRow">
                      <v-icon>add</v-icon>
                      Add row
                    </v-btn>  

                  </draggable>
                  <tfoot>
                    <tr>
                      <td colspan="2" class="text-right">TOTAL</td>
                      <td colspan="1" class="text-right">Total?</td>
                      <td></td>
                    </tr>
                  </tfoot>
                </table>
              </v-card-text>
            </v-card>
          </v-flex>
        </v-layout>
        
        <v-layout row>
          <v-flex xs12>
            <v-card>
              <v-card-title primary-title>
                <div>
                  <h3 class="headline mb-0">Payment Terms</h3>
                </div>
              </v-card-title>
              <v-card-text>
                <v-text-field
                    v-model="payName"
                    label="Name"
                    required
                  ></v-text-field>
                <v-text-field
                    v-model="bankName"
                    label="Bank Legal Name"
                    required
                  ></v-text-field>
                <v-text-field
                    v-model="bankAddress"
                    label="Bank Address"
                    required
                  ></v-text-field>
                <v-text-field
                    v-model="swift"
                    label="Swift # or Bic"
                    required
                  ></v-text-field>
                <v-text-field
                    v-model="inn"
                    label="Individual Tax Number"
                    required
                  ></v-text-field>
                <v-text-field
                    v-model="iban"
                    label="IBAN Number"
                    required
                  ></v-text-field>
              </v-card-text>
              <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn depressed large color="primary mr-2 mb-2 pr-5">
                  <v-icon dark left>print</v-icon>
                
                  Generate invoice
                </v-btn>
              </v-card-actions>
            </v-card>
          </v-flex>
        </v-layout>
      </v-container>
    </v-form>
  </v-app>
</template>

<script>
import draggable from "vuedraggable";
export default {
  components: {
    draggable
  },
  data() {
    return {
      elements: [
        { componentName: "ElementHeader", value: "First" },
        { componentName: "ElementHeader", value: "Second" }
      ],
      valid: false,
      menu: false,
      name: "",
      street: "",
      city: "",
      country: "",
      zip: "",
      phone: "",
      email: "",
      invoiceDate: null,
      invoiceID: "",
      project: "",
      department: "",
      payName: "",
      bankName: 'JSC CB "PRIVATBANK"',
      bankAddress: "1D HRUSHEVSKOHO STR., KYIV, 01001, UKRAINE ",
      swift: "PBANUA2X",
      inn: "",
      iban: "",
      nameRules: [
        v => !!v || "Name is required",
        v => v.length <= 10 || "Name must be less than 10 characters"
      ],
      emailRules: [
        v => !!v || "E-mail is required",
        v => /.+@.+/.test(v) || "E-mail must be valid"
      ],
      rows: [
        { description: "Something", price: 55.2 },
        { description: "Something else", price: 1255.2 }
      ],
      grandtotal: 0,
      delivery: 40
    }
  },
  computed: {
    total: function() {
      var t = 0;
      // $.each(this.rows, function(i, e) {
      //   t += accounting.unformat(e.total, ",");
      // });
      return t;
    },
    taxtotal: function() {
      var tt = 0;
      // $.each(this.rows, function(i, e) {
      //   tt += accounting.unformat(e.tax_amount, ",");
      // });
      return tt;
    }
  },
  methods: {
    addRow: function(index) {
      this.rows.push({
        description: '',
        price: ''
      })
    },
    removeRow: function(index) {
      this.rows.splice(index, 1);
    }
  },
  mounted() {}
};
</script>
