# H11-EM-1-CONSISTENCY-CHECK
Checks consistency of a 3x3 linear system using SymPy matrix rank
# Library used: SymPy (for symbolic math, matrices, and finding matrix rank)
# Assumption: The system has 3 linear equations with 3 variables (x, y, z)
from sympy import Matrix


def check_system_consistency(coeff_matrix, const_matrix):
    """Check if a system of linear equations is consistent using matrix rank."""
    # Join coefficient matrix (A) and constant matrix (B) side-by-side to get augmented matrix [A | B]
    augmented_matrix = coeff_matrix.row_join(const_matrix)

    # Calculate the rank of A and the rank of [A | B]
    rank_a = coeff_matrix.rank()
    rank_ab = augmented_matrix.rank()

    # Display the calculated ranks
    print("\n--- Rank Results ---")
    print("Rank of Coefficient Matrix (A):", rank_a)
    print("Rank of Augmented Matrix [A|B]:", rank_ab)

    # Apply Rouche-Capelli theorem to check consistency and number of solutions
    print("\n--- Conclusion ---")
    if rank_a == rank_ab:
        print("System is CONSISTENT (at least one solution exists).")
        # If rank equals the number of unknowns (columns in A), there is a unique solution
        if rank_a == coeff_matrix.cols:
            print("Type of Solution: UNIQUE solution.")
        else:
            print("Type of Solution: INFINITELY MANY solutions.")
    else:
        print("System is INCONSISTENT (no solution exists).")


def main():
    """Main function to set up matrices and run the consistency check."""
    # Coefficient matrix (3x3) representing coefficients of x, y, and z
    A = Matrix([
        [1, 2, 3],
        [2, 4, 6],
        [1, 1, 1]
    ])

    # Constant matrix (3x1) representing right-hand side values
    B = Matrix([
        [6],
        [12],
        [3]
    ])

    try:
        # Validate that matrix dimensions match for a 3-variable system
        if A.rows != 3 or A.cols != 3 or B.rows != 3 or B.cols != 1:
            raise ValueError("Matrices must be 3x3 for A and 3x1 for B.")

        check_system_consistency(A, B)

    except Exception as error:
        # Basic error handling so the program does not crash unexpectedly
        print("Error occurred while checking the system:", error)


# Run the program
if __name__ == "__main__":
    main()
