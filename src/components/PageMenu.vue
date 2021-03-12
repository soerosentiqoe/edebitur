<template>
  <div class='q-pa-md q-gutter-sm'>
    <q-tree
      :nodes='simple'
      accordion
      node-key='id'
      :expanded.sync='expanded'      
      :selected.sync='selected'
			text-color="primary" selected-color="negative"
    />
    <h5>{{selected}}</h5>
  </div>
</template>
<script>
export default {
  name: 'PageMenu',
  data() {
    return {
      simple: [
        {
          label: 'Administrator',
          id: 0,
          avatar: 'https://cdn.quasar.dev/img/boy-avatar.png',
          children: [
            {
              label: 'Rekening',
              id: 10,
              icon: 'eva-book-outline',
              children: [
                { label: 'Data', id: 11 },
                { label: 'Saldo', id: 12 }
              ]
            },
            {
              label: 'Debitur',
              id: 20,
              icon: 'eva-briefcase-outline',
              children: [
                { label: 'Pencairan', id: 21 },
                { label: 'Kartu', id: 22 }
              ]
            },

            {
              label: 'Referensi',
              id: 30,
              icon: 'eva-list',
              children: [
                {
                  label: 'Transaksi',
                  id: 31
                },
                { label: 'Bank', id: 32 },
                { label: 'Debitur', id: 33 }
              ]
            }
          ]
        }
      ],
      expanded: [0, 30],
      selected: ''
    };
  }
};
</script>
