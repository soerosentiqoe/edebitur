<template>
  <q-page class='flex full-width'>
    <div class='q-my-none q-card q-card--bordered q-card--flat no-shadow full-width'>
      <div class='q-toolbar row no-wrap items-center doc-example__toolbar'>
        <section id='Example--Basic' class='q-my-sm q-mr-md cursor-pointer text-subtitle1'>
          <div class='doc-card-title'>Transaksi</div>
        </section>
        <div class='q-space'></div>
        <div class='col-auto'>
          <q-btn dense flat icon="eva-plus-square-outline" color="primary"/>
					<q-btn dense flat icon="eva-trash-2-outline" class="q-pl-xs" color="negative"/>
        </div>
      </div>
      <hr
        role='separator'
        aria-orientation='horizontal'
        class='q-separator doc-example__separator q-separator q-separator--horizontal'
      />
      <div class='row'>
        <div class='q-pa-md full-width'>
          <q-table :data='data' :columns='columns' row-key='id' selection='single' dense />
        </div>
        <div class='q-pa-md full-width'>
          <q-card class='my-card'>
            <q-card-section>
              <q-form class='q-gutter-md'>
                <div class='row'>
                  <div class='full-width rounded-borders'>
                    Rekening:
                    <q-option-group
                      v-model='rekening'
                      :options='refrekening'
                      color='primary'
                      inline
                      dense
											class="q-pa-xs"
                    />
                  </div>
                </div>
                <div class='row'>
                  <div class='col-3 q-pr-md'>
                    <q-select
                      filled
                      v-model='model'
                      use-input
                      hide-selected
                      fill-input
                      input-debounce='0'
                      :options='options'
                      @filter='filterFn'
                      hint='Jenis Transaksi'
                      dense
                    >
                      <template v-slot:no-option>
                        <q-item>
                          <q-item-section class='text-grey'>No results</q-item-section>
                        </q-item>
                      </template>
                    </q-select>
                  </div>
                  <div class='col-2 q-pr-md'>
                    <q-input
                      filled
                      type='date'
                      hint='Tanggal Transaksi'
                      dense
                      label-color='primary'
                    />
                  </div>
                  <div class='col-7'>
                    <q-input hint='Uraian' filled autogrow dense />
                  </div>
                </div>
                <div class='row'>
                  <div class='col-3 q-pr-md'>
                    <q-input filled type='number' hint='Jumlah' dense />
                  </div>
                  <div class='col-2 q-pr-md'>
                    <div class='rounded-borders'>
                      D/K:
                      <q-option-group
                        v-model='dkvalue'
                        :options='dkArray'
                        color='primary'
                        inline
                        dense
                        hint='D/K'
                      />
                    </div>
                  </div>
                  <div class='col-4'>
                    <q-input dense filled hint='Debitur' disable>
                      <template v-slot:append>
                        <q-icon name='eva-layers-outline' />
                      </template>
                    </q-input>
                  </div>
                </div>

                <div>
                  <q-btn no-caps glossy dense icon='eva-save-outline' label='Simpan' type='submit' color="primary"/>
                  <q-btn
                    glossy
                    dense
                    icon='eva-close-circle-outline'
                    label='Reset'
                    type='reset'                                       
                    class='q-ml-sm'
										no-caps
										color="negative"
                  />
                </div>
              </q-form>
            </q-card-section>
            <q-separator dark />

            <!-- <q-card-actions>
              <q-btn-group>
                <q-btn color='secondary' glossy label='Rekam' />
                <q-btn color='secondary' glossy label='Ubah' />
                <q-btn color='secondary' glossy label='Hapus' />
              </q-btn-group>
            </q-card-actions>-->
          </q-card>
        </div>
      </div>
      <!---->
    </div>
  </q-page>
</template>

<script>
const stringOptions = ['Google', 'Facebook', 'Twitter', 'Apple', 'Oracle'];
export default {
  name: 'PageTransaksi',
  data() {
    return {
      model: null,
      options: stringOptions,
      dkvalue: 'Debet',
      dkArray: [
        {
          label: 'Debet',
          value: 'Debet'
        },
        {
          label: 'Kredit',
          value: 'Kredit'
        }
      ],
      rekening: 'BNI 1710197865 DK',
      refrekening: [
        {
          label: 'BNI 1710197865 DK',
          value: 'BNI 1710197865 DK'
        },
        {
          label: 'BNI 2104196434 OP',
          value: 'BNI 2104196434 OP'
        },
        {
          label: 'BRI 023001003386309 DK',
          value: 'BRI 023001003386309 DK'
        },
        {
          label: 'BRI 023001003411308 OP',
          value: 'BRI 023001003411308 OP'
        }
      ],
      tanggal: '2019/02/01',
      columns: [
        {
          name: 'tanggal',
          align: 'center',
          label: 'Tanggal',
          field: 'tanggal',
          sortable: true
        },
        { name: 'uraian', label: 'Uraian', field: 'uraian', sortable: true },
        { name: 'jenis', label: 'Jenis', field: 'jenis' },
        { name: 'rekening', label: 'Rekening', field: 'rekening' },
        { name: 'kelompok', label: 'Kelompok', field: 'kelompok' },
        {
          name: 'debet',
          label: 'Debet',
          field: 'debet',
          sortable: true,
          sort: (a, b) => parseInt(a, 10) - parseInt(b, 10)
        },
        {
          name: 'kredit',
          label: 'Kredit',
          field: 'kredit',
          sortable: true,
          sort: (a, b) => parseInt(a, 10) - parseInt(b, 10)
        }
      ],
      data: [
        {
          id: 1,
          tanggal: '2021-03-01',
          uraian: 'Provisi Khoirul Amin',
          jenis: 'Pendapatan Provisi',
          rekening: 'BRI 023001003411308 OP Pen',
          kelompok: 'L 00002',
          debet: '225.000',
          kredit: 0
        },
        {
          id: 2,
          tanggal: '2021-03-01',
          uraian: 'Provisi Khoirul Amin',
          jenis: 'Pendapatan Provisi',
          rekening: 'BRI 023001003411308 OP Pen',
          kelompok: 'L 00002',
          debet: '225.000',
          kredit: 0
        },
        {
          id: 3,
          tanggal: '2021-03-01',
          uraian: 'Provisi Khoirul Amin',
          jenis: 'Pendapatan Provisi',
          rekening: 'BRI 023001003411308 OP Pen',
          kelompok: 'L 00002',
          debet: '225.000',
          kredit: 0
        },
        {
          id: 4,
          tanggal: '2021-03-01',
          uraian: 'Provisi Khoirul Amin',
          jenis: 'Pendapatan Provisi',
          rekening: 'BRI 023001003411308 OP Pen',
          kelompok: 'L 00002',
          debet: '225.000',
          kredit: 0
        },
        {
          id: 5,
          tanggal: '2021-03-01',
          uraian: 'Provisi Khoirul Amin',
          jenis: 'Pendapatan Provisi',
          rekening: 'BRI 023001003411308 OP Pen',
          kelompok: 'L 00002',
          debet: '225.000',
          kredit: 0
        }
      ]
    };
  },
  methods: {
    filterFn(val, update, abort) {
      update(() => {
        const needle = val.toLowerCase();
        this.options = stringOptions.filter(
          v => v.toLowerCase().indexOf(needle) > -1
        );
      });
    }
  }
};
</script>
<style lang="sass">
.q-field__messages
	color: blue
</style>