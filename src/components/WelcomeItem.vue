<template>
  <div class="flex justify-center text-left mb-4">
    <i class="mr-4 pt-1">
      <slot name="icon"></slot>
    </i>
    <div class="max-w-lg">
      <h3 class="font-bold text-lg">
        <slot name="heading"></slot>
      </h3>
      <slot></slot>
    </div>
  </div>
</template>
