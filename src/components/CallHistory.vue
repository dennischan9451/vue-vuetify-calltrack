<template>
  <v-card>
    <v-card-text>
      <div class="mb-2">
        <span class="subtitle-2 black--text font-weight-bold mr-2 mt-2">0 CALLS FOUND</span>
        <span class="subtitle-2 font-weight-bold mr-2 mt-2">0 POOLED CALLS</span>
      </div>
      <v-divider class="black mb-2"></v-divider>
      <v-data-table
        :headers="headers"
        :items="calls"
        :items-per-page="itemsPerPage"
      >
        <template v-slot:[`item.date`]="{ item }">
          <span>Incoming</span><br>
          <a>{{ item.date }}</a>
        </template>
        <template v-slot:[`item.source`]="{ item }">
          <span class="font-weight-bold mr-1">Campaign:</span>{{ item.campaign }}<br>
          <span class="font-weight-bold mr-1">Client:</span>{{ item.client }}<br>
        </template>
        <template v-slot:[`item.call_details`]="{ item }">
          <span class="mr-6">From:</span><img src="@/assets/img/us.png">&nbsp;{{ item.from }}<br>
          <span class="mr-9">To:</span> <img src="@/assets/img/us.png">&nbsp;{{ item.to }}<br>
          <span class="mr-6">Rang:</span><img src="@/assets/img/us.png">&nbsp;{{ item.rang }}<br>
          <span class="mr-2">Caller ID:</span>{{ item.caller_id }}<br>
          <span class="mr-6">Label:</span>{{ item.label }}<br>
        </template>
        <template v-slot:[`item.city_state`]="{ item }">
          <span>{{ item.city }}, {{ item.state }}</span>
        </template>
        <template v-slot:[`item.status`]="{ item }">
          <v-chip
            color="green"
            dark
            class="status"
            small
          >
            {{ item.status }}
          </v-chip>
        </template>
        <template v-slot:[`item.recording`]="">
          <v-icon>
            mdi-play-circle
          </v-icon>
        </template>
        <template v-slot:[`item.actions`]="">
          <v-icon
            class="mr-2"
            @click="blackDlgVisiable = true"
          >
            mdi-close-thick
          </v-icon>
          <v-icon
            @click="noteDlgVisiable = true"
          >
            mdi-message-processing-outline
          </v-icon>
      </template>
      </v-data-table>
    </v-card-text>
    <v-dialog
      v-model="blackDlgVisiable"
      :max-width="variables.dlgMaxWidth"
    >
      <v-card>
        <v-card-title class="body-1">
          <v-icon class="mr-1" small>
            mdi-help-circle
          </v-icon>
          Question
        </v-card-title>
        <v-card-text>Are you sure you want to blacklist this number?</v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn
            color="green darken-1"
            text
            @click="blackDlgVisiable = false"
          >
            Yes
          </v-btn>
          <v-btn
            color="red darken-1"
            text
            @click="blackDlgVisiable = false"
          >
            No
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
    <v-dialog
      v-model="noteDlgVisiable"
      :max-width="variables.dlgMaxWidth"
    >
      <v-card>
        <v-card-title class="body-1">
          <v-icon class="mr-1" small>
            mdi-pencil
          </v-icon>
          Add Note
        </v-card-title>
        <v-card-text>
          <div class="font-weight-bold subtitle-1">Notes:</div>
          <div class="my-3">No notes found.</div>
          <span class="font-weight-bold subtitle-1">Contents:</span><br>
          <v-text-field
            outlined
          ></v-text-field>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn
            color="green darken-1"
            text
            @click="noteDlgVisiable = false"
          >
            Add
          </v-btn>
          <v-btn
            color="red darken-1"
            text
            @click="noteDlgVisiable = false"
          >
            Cancel
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-card>
</template>

<script>
import variables from '@/assets/scss/variable.scss'

export default {
  data () {
    return {
      variables,
      itemsPerPage: 10,
      blackDlgVisiable: false,
      noteDlgVisiable: false,
      headers: [
        { text: 'Date', sortable: false, value: 'date' },
        { text: 'Source', value: 'source', sortable: false },
        { text: 'Call Details', value: 'call_details', sortable: false },
        { text: 'City, State', value: 'city_state', sortable: false },
        { text: 'Duration', value: 'duration', sortable: false },
        { text: 'Status', value: 'status', sortable: false },
        { text: 'Recording', value: 'recording', sortable: false },
        { text: 'Actions', value: 'actions', sortable: false }
      ],
      calls: [
        {
          date: 'Sat 10/17 2020 1:20:12 PM',
          campaign: 'jacksonvilleapplianceexperts.com',
          client: '',
          from: '(914) 374-4290',
          to: '(904) 729-4487',
          rang: '904) 601-1701',
          caller_id: 'Christopher Mro',
          label: 'jacksonvilleapplianceexperts.com',
          city: 'ARDSLEY',
          state: 'NY',
          duration: '00:01:16',
          status: 'Completed', // completed
          recording: 'recording.mp3'
        },
        {
          date: 'Sat 10/17 2020 9:50:29 AM',
          campaign: 'jacksonvilleapplianceexperts.com',
          client: '',
          from: '(904) 616-0246',
          to: '(904) 729-4487',
          rang: '(904) 601-1701',
          caller_id: 'Shae Portnoy',
          label: 'jacksonvilleapplianceexperts.com',
          city: 'JACKSONVILLE',
          state: 'FL',
          duration: '00:00:50',
          status: 'Completed', // completed
          recording: 'recording.mp3'
        },
        {
          date: 'Sat 10/17 2020 8:13:02 AM',
          campaign: 'jacksonvilleapplianceexperts.com',
          client: '',
          from: '(904) 616-0246',
          to: '(904) 729-4487',
          rang: '(904) 601-1701',
          caller_id: 'Lanning C',
          label: 'jacksonvilleapplianceexperts.com',
          city: 'JACKSONVILLE',
          state: 'FL',
          duration: '00:00:50',
          status: 'Completed', // completed
          recording: 'recording.mp3'
        },
        {
          date: 'Sat 10/17 2020 8:11:41 AM',
          campaign: 'jacksonvilleapplianceexperts.com',
          client: '',
          from: '(904)616-0246',
          to: '(904)729-4487',
          rang: '(904)601-1701',
          caller_id: 'Lanning C',
          label: 'jacksonvilleapplianceexperts.com',
          city: 'JACKSONVILLE',
          state: 'FL',
          duration: '00:00:50',
          status: 'Completed', // completed
          recording: 'recording.mp3'
        },
        {
          date: 'Fri 10/16 2020 5:20:04 PM',
          campaign: 'jacksonvilleapplianceexperts.com',
          client: '',
          from: '(904)616-0246',
          to: '(904)729-4487',
          rang: '(904)601-1701',
          caller_id: 'Shae Portnoy',
          label: 'jacksonvilleapplianceexperts.com',
          city: 'JACKSONVILLE',
          state: 'FL',
          duration: '00:00:50',
          status: 'Completed', // completed
          recording: 'recording.mp3'
        },
        {
          date: 'Fri 10/16 2020 3:56:41 PM',
          campaign: 'jacksonvilleapplianceexperts.com',
          client: '',
          from: '(904)616-0246',
          to: '(904)729-4487',
          rang: '(904)601-1701',
          caller_id: 'Shae Portnoy',
          label: 'jacksonvilleapplianceexperts.com',
          city: 'JACKSONVILLE',
          state: 'FL',
          duration: '00:00:50',
          status: 'Completed', // completed
          recording: 'recording.mp3'
        },
        {
          date: 'Fri 10/16 2020 3:56:41 PM',
          campaign: 'jacksonvilleapplianceexperts.com',
          client: '',
          from: '(904)616-0246',
          to: '(904)729-4487',
          rang: '(904)601-1701',
          caller_id: 'Shae Portnoy',
          label: 'jacksonvilleapplianceexperts.com',
          city: 'JACKSONVILLE',
          state: 'FL',
          duration: '00:00:50',
          status: 'Completed', // completed
          recording: 'recording.mp3'
        }
      ]
    }
  }
}
</script>

<style lang="scss" scoped>
@import "@/assets/scss/variable.scss";
::v-deep .v-data-table {
  thead th {
    font-size: $FS14 !important;
  }
  tbody td {
    font-size: $FS12 !important;
    padding: 5px 16px !important;
  }
}
::v-deep .status span {
  font-size: $FS12 !important;
}
::v-deep .v-dialog .v-card__text {
  border-top: 1px solid lightgray;
  border-bottom: 1px solid lightgray;
  padding-top: 10px !important;
}
</style>
