<template>
  <div
    v-if="field.authorizedToView"
    class="relative"
    :dusk="field.resourceName + '-index-component'"
    :data-relationship="viaRelationship"
  >
    <template v-if="!hasRelation">
      <Heading :level="1" class="mb-3 flex items-center">{{
        field.singularLabel
      }}</Heading>
      <Card>
        <IndexEmptyDialog
          :create-button-label="createButtonLabel"
          :singular-name="singularName"
          :resource-name="field.resourceName"
          :via-resource="resourceName"
          :via-resource-id="viaResourceId"
          :via-relationship="viaRelationship"
          :relationship-type="field.relationshipType"
          :authorized-to-create="false"
          :authorized-to-relate="false"
        />
      </Card>
    </template>
    <div v-else>
      <ResourceDetail
        :resource-name="field.resourceName"
        :resource-id="field.hasOneThroughId"
        :via-resource="resourceName"
        :via-resource-id="viaResourceId"
        :via-relationship="viaRelationship"
        :relationship-type="field.relationshipType"
        :show-view-link="true"
      />
    </div>
  </div>
</template>

<script>
export default {
  props: ['resourceName', 'resourceId', 'resource', 'field'],

  computed: {
    authorizedToCreate() {
      return this.field.authorizedToCreate
    },

    createButtonLabel() {
      return this.field.createButtonLabel
    },

    hasRelation() {
      return this.field.hasOneThroughId != null
    },

    singularName() {
      return this.field.singularLabel
    },

    viaResourceId() {
      return this.resource.id.value
    },

    viaRelationship() {
      return this.field.hasOneThroughRelationship
    },
  },
}
</script>
