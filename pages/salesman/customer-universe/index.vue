<template>
  <div>
    <salesman-layout :extensionSlot="true" :prominentBar="false">
      <template #pageToolbars>
        <back-button class="mr-2" />
        <div class="title font-weight-black">Customer Universe</div>
        <v-spacer></v-spacer>
        <v-menu offset-y>
          <template v-slot:activator="{ on }">
            <v-btn small icon v-on="on">
              <v-icon>mdi-dots-vertical</v-icon>
            </v-btn>
          </template>
          <v-list>
            <v-list-item> </v-list-item>
          </v-list>
        </v-menu>
      </template>

      <template #extension-slot>
        <v-tabs centered dark v-model="tab">
          <v-tab key="#total">
            Total
            <v-badge
              color="secondary"
              dark
              :content="getAllOutlets ? getAllOutlets.length : 0"
            ></v-badge>
          </v-tab>
          <v-tab key="#active">Active</v-tab>
          <v-tab key="#pending">Pending</v-tab>
        </v-tabs>
      </template>

      <template #content>
        <div>
          <v-tabs-items v-model="tab">
            <v-tab-item key="total">
              <v-container>
                <v-row>
                  <v-col
                    v-for="outlet in getAllOutlets"
                    :key="outlet._id"
                    xs="12"
                    sm="12"
                    md="4"
                  >
                    <customer-card>
                      <template #uniqueId>{{ outlet.uniqueId }}</template>
                      <template #name>{{ outlet.name }}</template>
                      <template #owner>{{
                        outlet.owner.firstName + " " + outlet.owner.lastName
                      }}</template>
                      <template #contact>
                        {{ outlet.outletContact.telephone }}
                      </template>
                    </customer-card>
                  </v-col>
                </v-row>
              </v-container>
            </v-tab-item>
            <v-tab-item key="active">active outlets here ..</v-tab-item>
            <v-tab-item key="pending">pending outlets here</v-tab-item>
          </v-tabs-items>
        </div>
      </template>
    </salesman-layout>
  </div>
</template>
<script>
import CustomerCard from "~/components/CustomerCard";
import BackButton from "~/components/BackButton";
import SalesmanLayout from "~/components/SalesmanLayout";
import allOutlets from "~/apollo/queries/allOutlets";
export default {
  name: "OutletsPage",
  layout: "salesman-page",
  data() {
    return {
      tab: null
    };
  },
  apollo: {
    getAllOutlets: {
      query: allOutlets,
      prefetch: true
    }
  },
  components: {
    CustomerCard,
    BackButton,
    SalesmanLayout
  }
};
</script>

<style scoped></style>
