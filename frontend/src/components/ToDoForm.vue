<script setup lang="ts">
    import {Form as VeeForm, Field as VeeField, ErrorMessage as VeeErrorMessage} from 'vee-validate'
    import * as Z from 'zod'
    import { toTypedSchema } from '@vee-validate/zod'

const TODO_SCHEMA = Z.object ({
    title: Z.string().min(3).max(100),
    description: Z.string().max(1000).default('')
    })

const schema =toTypedSchema(TODO_SCHEMA)

async function onSubmit(values: any) {
    console.log(values)
    const body = {
        ...values,
        completed: false
    }
    const response = await fetch('http://localhost:6969/todos', { method: 'POST' , body:JSON.stringify(body), headers: {
        'Content-Type': 'application/json'
    } })
    window.location.reload()
}
</script>

<template>
    <VeeForm class="flex flex-col items-start max-w-md gap-2 mx-auto my-3" @submit="onSubmit" :validation-schema="schema">
        <label class="flex flex-col w-full gap-1">Title
        <VeeField class="px-3 py-2 border rounded bg-slate-50 border-slate-300" name="title" placeholder="title"/>
        <VeeErrorMessage name="title" class="text-red-500"/>
    </label>
    <label class="flex flex-col w-full gap-1">Description
        <VeeField class="px-3 py-2 border rounded bg-slate-50 border-slate-300" name="description" placeholder="description"/>
        <VeeErrorMessage class="text-red-500" name="password"/>
    </label>
        <button class="px-3 py-2 rounded  bg-slate-500 text-slate-50">submit</button>
    </VeeForm>
</template>