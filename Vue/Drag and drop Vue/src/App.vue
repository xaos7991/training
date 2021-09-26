<template>
  <div :class="$style.root">
    <Category
      v-for="category in categories"
      :title="category.title"
      :key="category.id"
      @drop="onDrop($event, category.id)"
      @dragover.prevent
      @dragenter.prevent
    >
      <CategoryItem
        v-for="item in items.filter((x) => x.categoryId === category.id)"
        :title="`${item.title} ${item.id}`"
        :key="item.id"
        @dragstart="onDragStart($event, item)"
        class="draggable"
        draggable="true"
      />
    </Category>
  </div>
</template>

<script>
import { ref } from 'vue';
import Category from '@/components/Category.vue';
import CategoryItem from '@/components/CategoryItem.vue';

export default {
  name: 'App',
  components: {
    Category,
    CategoryItem,
  },
  setup() {
    const items = ref([
      {
        id: 0,
        title: 'Some tasks',
        categoryId: 0,
      },
      {
        id: 1,
        title: 'Some tasks',
        categoryId: 0,
      },
      {
        id: 2,
        title: 'Some tasks',
        categoryId: 1,
      },
      {
        id: 3,
        title: 'Some tasks',
        categoryId: 2,
      },
    ]);
    const categories = ref([
      {
        id: 0,
        title: 'Open',
      },
      {
        id: 1,
        title: 'In progress',
      },
      {
        id: 2,
        title: 'Done',
      },
    ]);

    function onDragStart(e, item) {
      e.dataTransfer.dropEffect = 'move';
      e.dataTransfer.effectAllowed = 'move';
      e.dataTransfer.setData('itemId', item.id);
    }

    function onDrop(e, categoryId) {
      const itemId = parseInt(e.dataTransfer.getData('itemId'));
      const item = items.value.find((x) => x.id === itemId);
      item.categoryId = categoryId;
    }

    return {
      items,
      categories,
      onDragStart,
      onDrop,
    };
  },
};
</script>

<style module>
.root {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  gap: 20px;
}
</style>
