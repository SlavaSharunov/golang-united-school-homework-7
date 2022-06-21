package coverage

import (
	"os"
	"reflect"
	"strconv"
	"testing"
	"time"
)

// DO NOT EDIT THIS FUNCTION
func init() {
	content, err := os.ReadFile("students_test.go")
	if err != nil {
		panic(err)
	}
	err = os.WriteFile("autocode/students_test", content, 0644)
	if err != nil {
		panic(err)
	}
}

// WRITE YOUR CODE BELOW
func date(n int) time.Time {
	return time.Date(1990+n, 1, 0, 0, 0, 0, 0, time.UTC)
}

var testPersons People

const N = 10

func createPerson() {
	testPersons = make([]Person, 0)
	n := 0
	for n < N {
		testPersons = append(testPersons, Person{firstName: strconv.Itoa(n),
			lastName: strconv.Itoa(n),
			birthDay: date(n)})
		n += 1
	}
}

func TestLenOK(t *testing.T) {
	createPerson()
	got := testPersons.Len()
	if got != N {
		t.Errorf("TestLenOK expected: %d, got %d", N, got)
	}
}

func TestLessOK(t *testing.T) {
	createPerson()
	got := testPersons.Less(4, 6)
	if got != false {
		t.Errorf("TestLenOK expected: false, got %t", got)
	}
}

func TestSwapOK(t *testing.T) {
	createPerson()
	first := testPersons[4]
	second := testPersons[6]
	testPersons.Swap(4, 6)
	if first != testPersons[6] {
		t.Errorf("TestSwapOK expected: %+v, got %+v", first, testPersons[6])
	}
	if second != testPersons[4] {
		t.Errorf("TestSwapOK expected: %+v, got %+v", second, testPersons[4])
	}
}

func TestNewMatrixOK(t *testing.T) {
	_, err := New("a35")
	if err != nil {
		t.Errorf("Wrong String Error")
	}

	_, err = New("1 1 \n 2")
	if err != nil {
		t.Errorf("Wrong Matrix Error")
	}

	matrix, err := New("1 1 \n 2 3")
	expects := &Matrix{2, 2, []int{1, 1, 2, 3}}

	if err != nil || matrix.cols != expects.cols || matrix.rows != expects.rows {
		t.Errorf("Wrong Empty Matrix")
	}
}

func Equal(a, b []int) bool {
	if len(a) != len(b) {
		return false
	}
	for i, v := range a {
		if v != b[i] {
			return false
		}
	}
	return true
}

func TestRows(t *testing.T) {
	matrix := &Matrix{2, 2, []int{4, 5, 6, 7}}
	expects := [][]int{{4, 5}, {6, 7}}

	actual := matrix.Rows()

	if !Equal(actual[0], expects[0]) || !Equal(actual[1], expects[1]) {
		t.Errorf("Wrong Rows Matrix")
	}
}

func TestCols(t *testing.T) {
	matrix := &Matrix{3, 3, []int{1, 10, 100, 2, 20, 200, 3, 30, 300}}
	expects := [][]int{{1, 2, 3}, {10, 20, 30}, {100, 200, 300}}

	actual := matrix.Cols()

	if !Equal(actual[0], expects[0]) || !Equal(actual[1], expects[1]) || !Equal(actual[2], expects[2]) {
		t.Errorf("Wrong Cols Matrix")
	}
}

func TestSet(t *testing.T) {
	matrix := &Matrix{3, 3, []int{1, 10, 100, 2, 20, 200, 3, 30, 300}}
	expectsMatrix := []int{1, 10, 100, 2, 10000000, 200, 3, 30, 300}

	actual := matrix.Set(1, 1, 10000000)

	if !actual || !reflect.DeepEqual(matrix.data, expectsMatrix) {
		t.Errorf("Wrong Set Matrix")
	}

	actual = matrix.Set(-1, 2, 10000000)
	if actual {
		t.Errorf("Wrong Set Error")
	}
}
