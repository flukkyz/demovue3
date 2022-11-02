<template>
  <v-app>
    <v-main>
      <v-container fluid>
        <v-card>
          <v-card-text>
            <search-input 
            label="ค้นหาเธอ" 
            color="primary"
            @search="onSearch"
            />
    
          </v-card-text>
        </v-card>
        
      </v-container>
      
          <!-- <hello-world /> -->
    </v-main>
  </v-app>
</template>

<script setup lang="ts">
// import HelloWorld from '@/components/HelloWorld.vue'
import SearchInput from '@/components/SearchInput.vue'

type ValidationResult = string | boolean;
type ValidationRule = ValidationResult | PromiseLike<ValidationResult> | ((value: any) => ValidationResult) | ((value: any) => PromiseLike<ValidationResult>)

const rule: ValidationRule[] = [
  (v: any) => v === 'a' || 'กรุณากรอกชื่อขนาดรูป'
]

const onSearch = (data: string) => {
  console.log('SEARCH',data);    
}
</script>
