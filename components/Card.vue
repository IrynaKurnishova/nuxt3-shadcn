<template>
  <Card>
    <CardHeader class="px-2 pt-4 pb-2">
      <div class="flex justify-between items-center">
        <p>{{card.title}}</p>
        <Badge class="bg-green-400">{{'+' + card.progression + '%'}}</Badge>
      </div>
    </CardHeader>
    <CardContent class="flex items-center justify-end border-b pt-0 px-4 pb-2">
      <div class="text-[48px] font-[800]">
        <span class="text-neutral-300">$</span>
        <span>{{card.amount}}</span>
      </div>
    </CardContent>
    <CardFooter class="flex gap-2 py-2 px-2 items-center justify-between">
      <div class="w-8 h-8 bg-neutral-100 rounded flex items-center justify-center">
        <Icon size="20" :name="card.icon" color="black"/>
      </div>
      <p class="grow text-xs">{{card.description}}</p>
      <Button variant="outline">{{card.label}}</Button>
    </CardFooter>
  </Card>
</template>

<script setup>
import {Badge} from "@/components/ui/badge"
import {
  Card,
  CardContent,
  CardFooter,
  CardHeader
} from '@/components/ui/card'

const props = defineProps(["card"])
</script>
