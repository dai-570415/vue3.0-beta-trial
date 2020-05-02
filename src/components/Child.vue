<template>
    <div class="child">
        <button @click="upperCaseMessage">toUpperCase</button>
    </div>
</template>

<script lang="ts">
    import { defineComponent, SetupContext } from 'vue';

    type Props = {
        message: string;
    };

    export default defineComponent({
        name: 'Child',
        props: {
            message: {
                type: String,
                default: 'default Value'
            }
        },
        setup(props: Props, context: SetupContext) {
            const upperCaseMessage = () => {
                context.emit('change-message', props.message.toUpperCase());
            };

            return {
                upperCaseMessage
            };
        }
    });
</script>