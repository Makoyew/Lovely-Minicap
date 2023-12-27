<script setup>
import NewLayout from '@/Layouts/NewLayout.vue';
import Navbar from '@/Components/Navbar.vue';
</script>

<template>
    <NewLayout>
        <Navbar />
        <div class="py-12">
            <div class="px-4 mx-auto max-w-7xl">
                <!-- Banner -->
                <div class="p-4 mb-6 text-white bg-green-500 rounded-md">
                    <h1 class="text-3xl font-semibold">Discover Your Blooming Oasis</h1>
                    <p class="text-sm">Cultivate joy and serenity in your vibrant garden.</p>
                </div>

                <!-- Main Content Grid -->
                <div class="grid grid-cols-1 gap-8 md:grid-cols-2">
                    <!-- Garden Overview -->
                    <div class="relative p-6 overflow-hidden bg-white rounded-lg shadow-md">
                        <img src="https://images.fineartamerica.com/images-medium-large-5/sunrise-over-the-garden-preappy.jpg" alt="Garden Overview" class="object-cover w-full mb-4 rounded-md h-60" />
                        <h2 class="mb-2 text-xl font-semibold text-green-700">
                            Garden Overview
                        </h2>
                        <!-- Placeholder Content -->
                        <div class="flex items-center justify-between mt-2">
                            <div class="text-gray-600">Total Plants:</div>
                            <div class="text-lg font-semibold text-green-700">25</div>
                        </div>
                        <div class="flex items-center justify-between mt-2">
                            <div class="text-gray-600">Healthy Plants:</div>
                            <div class="text-lg font-semibold text-green-700">20</div>
                        </div>
                    </div>

                    <!-- User Profile -->
                    <div class="relative p-6 overflow-hidden bg-white rounded-lg shadow-md">
                        <img src="https://upload.wikimedia.org/wikipedia/commons/9/92/Garden_Background.jpg" alt="Profile Banner" class="object-cover w-full mb-4 rounded-md h-60" />
                        <h2 class="mb-2 text-xl font-semibold text-green-700">
                            My Profile
                        </h2>
                        <div class="flex items-center">
                            <img src="https://png.pngtree.com/template/20191024/ourmid/pngtree-flower-pot-and-plant-logo-growth-vector-logo-image_322946.jpg" alt="Plant Image" class="w-16 h-16 rounded-full" />
                            <div class="ml-4">
                                <p class="text-lg font-semibold text-green-700">Lovely Jane Pelayre</p>
                                <p class="text-green-600">Passionate Gardener</p>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Featured Plants Section -->
                <div class="p-6 mt-8 bg-white rounded-lg shadow-md">
                    <h2 class="mb-4 text-xl font-semibold text-green-700">
                        Featured Plants
                    </h2>
                    <!-- Add your featured plants with images and descriptions -->
                    <div class="grid grid-cols-1 gap-8 md:grid-cols-2 lg:grid-cols-3">
                        <!-- Plant 1 -->
                        <div class="p-4 bg-gray-200 rounded-md">
                            <img src="https://assets.hvmag.com/2023/05/GfOXqtm3-Sunflower-Fields.jpg" alt="Featured Plant 1" class="object-cover w-full h-32 mb-2 rounded-md" />
                            <p class="text-lg font-semibold text-green-700">Sunflower</p>
                            <p class="text-gray-600">Bright and cheerful, perfect for sunny spots.</p>
                        </div>
                        <!-- Plant 2 -->
                        <div class="p-4 bg-gray-200 rounded-md">
                            <img src="https://inaturalist-open-data.s3.amazonaws.com/photos/78919895/original.jpeg" alt="Featured Plant 2" class="object-cover w-full h-32 mb-2 rounded-md" />
                            <p class="text-lg font-semibold text-green-700">Fiddle Leaf Fig</p>
                            <p class="text-gray-600">A trendy indoor plant with large, glossy leaves.</p>
                        </div>
                        <!-- Plant 3 -->
                        <div class="p-4 bg-gray-200 rounded-md">
                            <img src="https://img1.wsimg.com/isteam/ip/f945cf36-7f90-484f-871a-bf0c2daf6c2e/66B3BA60-5666-40A7-8039-804063217011.jpeg" alt="Featured Plant 3" class="object-cover w-full h-32 mb-2 rounded-md" />
                            <p class="text-lg font-semibold text-green-700">Succulent Collection</p>
                            <p class="text-gray-600">Easy to care for and adds a touch of desert charm.</p>
                        </div>
                    </div>
                </div>

                <!-- Garden Tips Container -->
                <div class="p-6 mt-8 bg-white rounded-lg shadow-md">
                    <h2 class="mb-4 text-xl font-semibold text-green-700">
                        Garden Tips
                    </h2>
                    <!-- Add gardening tips or advice here -->
                    <ul class="pl-6 list-disc">
                        <li class="text-gray-700">Choose the right plants for your climate.</li>
                        <li class="text-gray-700">Provide proper sunlight and water for optimal growth.</li>
                        <li class="text-gray-700">Prune regularly to maintain plant health.</li>
                        <li class="text-gray-700">Experiment with different plant arrangements for aesthetic appeal.</li>
                    </ul>
                </div>
            </div>
        </div>
    </NewLayout>
</template>
