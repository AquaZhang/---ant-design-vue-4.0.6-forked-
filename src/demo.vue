<template>
  <!-- ... -->
  <a-form-item
    :name="['users', index, 'treeSelect']"
    :rules="{
      required: true,
      message: 'Missing tree selection',
    }"
  >
    <a-tree-select
      v-model:value="user.treeSelect"
      style="width: 200px"
      tree-checkable
      allow-clear
      max-tag-count="responsive"
      :tree-data="customTreeData"
      placeholder="Select from tree"
      @change="handleTreeSelectChange(index)"
      tree-node-filter-prop="label"
    ></a-tree-select>
  </a-form-item>
  <!-- ... -->
</template>
<script>
import { reactive, ref } from "vue";

const customTreeData = [
  {
    label: "Option 1",
    value: "option1",
  },
  {
    label: "Option 2",
    value: "option2",
  },
  // Add more tree data as needed
];

const formRef = ref();

const dynamicValidateForm = reactive({
  users: [],
});

const removeUser = (item) => {
  const index = dynamicValidateForm.users.indexOf(item);
  if (index !== -1) {
    dynamicValidateForm.users.splice(index, 1);
  }
};

const addUser = () => {
  dynamicValidateForm.users.push({
    first: "",
    last: "",
    treeSelect: "", // Initialize treeSelect
    id: Date.now(),
  });
};

const handleTreeSelectChange = (index) => {
  // Handle tree select change for the specific user
  console.log(
    `Tree select changed for user ${index}:`,
    dynamicValidateForm.users[index].treeSelect
  );
};

const onFinish = (values) => {
  console.log("Received values of form:", values);
  console.log("dynamicValidateForm.users:", dynamicValidateForm.users);
};
</script>