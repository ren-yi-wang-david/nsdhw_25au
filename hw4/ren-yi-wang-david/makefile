CXX := g++
CXXFLAGS := -O3 -std=c++17 -fPIC
PYTHON := python3

# 保留 pybind11 的 -I 標誌
PY_CPPFLAGS := $(shell $(PYTHON) -m pybind11 --includes)
# 乾淨的一行 Python：若有 numpy 則輸出 -I<路徑>，否則空
NUMPY_I := $(shell $(PYTHON) -c "import importlib.util, sys; \
spec = importlib.util.find_spec('numpy'); \
print('-I'+__import__('numpy').get_include() if spec else '')")

PYTHON_LDFLAGS := $(shell $(PYTHON)-config --ldflags)
TARGET := _matrix$(shell $(PYTHON)-config --extension-suffix)

MKL_INC := /usr/include/mkl
MKL_LIB := -lmkl_rt -lpthread -lm -ldl
OPENBLAS_LIB := -lopenblas -lpthread -lm

ifeq ($(wildcard $(MKL_INC)/mkl.h),)
    LIBS := $(OPENBLAS_LIB)
    CXXFLAGS += -DUSE_OPENBLAS
    $(info >>> Using OpenBLAS backend)
else
    LIBS := $(MKL_LIB)
    CXXFLAGS += -DUSE_MKL -I$(MKL_INC)
    $(info >>> Using Intel MKL backend)
endif

all: $(TARGET)

$(TARGET): matrix.cpp
	$(CXX) $(CXXFLAGS) $(PY_CPPFLAGS) $(NUMPY_I) \
		-shared matrix.cpp -o $(TARGET) \
		$(PYTHON_LDFLAGS) $(LIBS)

clean:
	rm -f $(TARGET)
