class MemoryBlock:
    def __init__(self, size):
        self.size = size  # Size of the memory block
        self.used = False  # Indicates if the block is currently used
        self.remaining_size = size  # Keeps track of remaining size in the block

    def allocate(self, process_size):
        """Allocates a process to this memory block if it fits."""
        if self.remaining_size >= process_size:
            self.used = True
            self.remaining_size -= process_size
            return True
        return False

    def free(self):
        """Frees the memory block."""
        self.used = False
        self.remaining_size = self.size

    def __repr__(self):
        return f"Block(size={self.size}, used={self.used}, remaining={self.remaining_size})"


class NextFitAllocator:
    def __init__(self, memory_blocks):
        self.memory_blocks = memory_blocks  # List of MemoryBlock objects
        self.last_allocated_block = -1  # Points to the last allocated block

    def allocate(self, process_size):
        """Allocates a process using the Next Fit algorithm."""
        num_blocks = len(self.memory_blocks)
        
        # Start from the last allocated block and search for a suitable block
        for i in range(self.last_allocated_block + 1, num_blocks):
            if self.memory_blocks[i].allocate(process_size):
                self.last_allocated_block = i  # Update last allocated block
                return f"Process of size {process_size} allocated to block {i+1}."
        
        # If no suitable block is found, try from the beginning up to last allocated block
        for i in range(0, self.last_allocated_block + 1):
            if self.memory_blocks[i].allocate(process_size):
                self.last_allocated_block = i  # Update last allocated block
                return f"Process of size {process_size} allocated to block {i+1}."

        return f"Process of size {process_size} could not be allocated."

    def free(self, block_index):
        """Frees the specified memory block."""
        if 0 <= block_index < len(self.memory_blocks):
            self.memory_blocks[block_index].free()
            print(f"Block {block_index + 1} freed.")

    def display_memory(self):
        """Displays the current state of the memory blocks."""
        print("\nCurrent Memory Blocks:")
        for i, block in enumerate(self.memory_blocks):
            print(f"Block {i+1}: Size = {block.size}, Used = {block.used}, Remaining = {block.remaining_size}")



if __name__ == "__main__":
    # Create memory blocks
    memory_blocks = [MemoryBlock(100), MemoryBlock(200), MemoryBlock(300), MemoryBlock(400)]

    # Create a NextFitAllocator instance
    allocator = NextFitAllocator(memory_blocks)

    # Display initial memory state
    allocator.display_memory()

    # Allocate processes
    print(allocator.allocate(50))  # Process of size 50
    print(allocator.allocate(150))  # Process of size 150
    print(allocator.allocate(250))  # Process of size 250
    print(allocator.allocate(100))  # Process of size 100

    # Display memory after allocations
    allocator.display_memory()

    # Free a block and try to allocate again
    allocator.free(1)  # Free block 2
    print(allocator.allocate(100))  # Process of size 100 after freeing block 2

    # Display memory after freeing a block
    allocator.display_memory()
