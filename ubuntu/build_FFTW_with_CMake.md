FFTW_VERSION=3.3.9
curl -L http://www.fftw.org/fftw-${FFTW_VERSION}.tar.gz | tar xz
mkdir build && cd $_
cmake -DBUILD_SHARED_LIBS=OFF -DENABLE_OPENMP=ON -DENABLE_THREADS=ON -DENABLE_LONG_DOUBLE=ON ../fftw-${FFTW_VERSION}
make -j $(nproc) install
rm -r *
cmake -DBUILD_SHARED_LIBS=OFF -DENABLE_OPENMP=ON -DENABLE_THREADS=ON -DENABLE_FLOAT=ON -DENABLE_SSE=ON -DENABLE_SSE2=ON -DENABLE_AVX=ON -DENABLE_AVX2=ON ../fftw-${FFTW_VERSION}
make -j $(nproc) install
rm -r *
cmake -DBUILD_SHARED_LIBS=OFF -DENABLE_OPENMP=ON -DENABLE_THREADS=ON -DENABLE_SSE=ON -DENABLE_SSE2=ON -DENABLE_AVX=ON -DENABLE_AVX2=ON ../fftw-${FFTW_VERSION}
make -j $(nproc) install
