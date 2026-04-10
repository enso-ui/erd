<script>
import { debounce } from 'lodash';

export default {
    name: 'Erd',

    props: {
        debounce: {
            type: Number,
            default: 1,
        },
    },

    data: () => ({
        width: null,
        height: null,
        erd: null,
    }),

    mounted() {
        const updateSize = debounce(([entry]) => {
            this.width = entry.contentRect.width;
            this.height = entry.contentRect.height;
        }, this.debounce);

        this.erd = new ResizeObserver(updateSize);
        this.erd.observe(this.$el);
    },

    beforeUnmount() {
        this.erd?.disconnect();
        this.erd = null;
    },

    render() {
        return this.$slots.default({
            width: this.width,
            height: this.height,
        });
    },
};
</script>
