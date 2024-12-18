# Crate-Value-Sum-Challenge

In a large warehouse, there are 106 crates numbered sequentially from 1 to 106, with each crate’s value matching its number. However, due to certain conditions, the values of crates within specified ranges [L, R] are set to zero. Given N such ranges, which may overlap, can you determine the total sum of all crate values from 1 to 106 after applying these conditions?

def crate_value_sum(n, ranges):
    # Total sum of numbers from 1 to 10^6
    MAX_CRATES = 10**6
    total_sum = MAX_CRATES * (MAX_CRATES + 1) // 2
    
    # Sort ranges by start, and then by end
    ranges.sort()
    
    # Merge overlapping ranges
    merged_ranges = []
    for l, r in ranges:
        if not merged_ranges or merged_ranges[-1][1] < l - 1:
            merged_ranges.append((l, r))
        else:
            merged_ranges[-1] = (merged_ranges[-1][0], max(merged_ranges[-1][1], r))
    
    # Calculate the sum of all zeroed values
    zeroed_sum = 0
    for l, r in merged_ranges:
        zeroed_sum += (r * (r + 1) // 2) - ((l - 1) * l // 2)
    
    # Calculate the remaining sum
    remaining_sum = total_sum - zeroed_sum
    return remaining_sum

# Input Handling
if __name__ == "__main__":
    n = int(input())
    ranges = [tuple(map(int, input().split())) for _ in range(n)]
    print(crate_value_sum(n, ranges))
