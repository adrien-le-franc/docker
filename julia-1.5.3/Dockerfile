FROM continuumio/anaconda3:5.3.0

RUN apt-get update && \
  	apt-get install -y --no-install-recommends wget build-essential hdf5-tools procps unzip default-jre && \
  	rm -rf /var/lib/apt/lists/* 

# install Julia

ENV JULIA_DEPOT_PATH=/opt/julia
ENV JULIA_PKGDIR=/opt/julia
ENV JULIA_VERSION=1.5.3

RUN mkdir /opt/julia-${JULIA_VERSION} && \
	cd /tmp && \
	wget -q --no-check-certificate https://julialang-s3.julialang.org/bin/linux/x64/`echo ${JULIA_VERSION} | cut -d. -f 1,2`/julia-${JULIA_VERSION}-linux-x86_64.tar.gz && \
	tar xzf julia-${JULIA_VERSION}-linux-x86_64.tar.gz -C /opt/julia-${JULIA_VERSION} --strip-components=1 && \
    rm /tmp/julia-${JULIA_VERSION}-linux-x86_64.tar.gz

RUN ln -fs /opt/julia-*/bin/julia /usr/local/bin/julia

# install and precompile Julia packages

RUN julia -e 'import Pkg; Pkg.update()' && \
	julia -e 'import Pkg; Pkg.add("IJulia")' && \
	julia -e 'import Pkg; Pkg.add("HDF5")' && \
	julia -e 'import Pkg; Pkg.add("Mmap")' && \
	julia -e 'import Pkg; Pkg.add("CodecZlib")' && \
	julia -e 'import Pkg; Pkg.add("JLD")' && \
	julia -e 'import Pkg; Pkg.add("JLD2")' && \
	julia -e 'import Pkg; Pkg.add("FileIO")' && \
	julia -e 'import Pkg; Pkg.add("Revise")' && \
	julia -e 'import Pkg; Pkg.add("CSV")' && \
	julia -e 'import Pkg; Pkg.add("DataFrames")' && \
	julia -e 'import Pkg; Pkg.add("Plots")' && \
	julia -e 'import Pkg; Pkg.add("StatsPlots")' && \
	julia -e 'import Pkg; Pkg.add("EllipsisNotation")' && \
	julia -e 'import Pkg; Pkg.add("ProgressMeter")' && \
	julia -e 'import Pkg; Pkg.add("ArgParse")' && \
	julia -e 'import Pkg; Pkg.add("Clustering")' && \
	julia -e 'import Pkg; Pkg.add("StatsBase")' && \
	julia -e 'import Pkg; Pkg.add("Interpolations")' && \
	julia -e 'import Pkg; Pkg.add("Polynomials")' && \
	julia -e 'import Pkg; Pkg.add("Distributions")' 

RUN julia -e 'using IJulia; IJulia.installkernel("Julia nodeps", "--depwarn=no")' && \
	julia -e 'using HDF5' && \
	julia -e 'using Mmap' && \
	julia -e 'using CodecZlib' && \
	julia -e 'using JLD' && \
	julia -e 'using JLD2' && \
	julia -e 'using FileIO' && \
	julia -e 'using Revise' && \
	julia -e 'using CSV' && \
	julia -e 'using DataFrames' && \
	julia -e 'using Plots' && \
	julia -e 'using StatsPlots' && \
	julia -e 'using EllipsisNotation' && \
	julia -e 'using ProgressMeter' && \
	julia -e 'using ArgParse' && \
	julia -e 'using Clustering' && \
	julia -e 'using StatsBase' && \
	julia -e 'using Interpolations' && \
	julia -e 'using Polynomials' && \
	julia -e 'using Distributions'

# install Clp solver and JuMP for LP problems

RUN julia -e 'import Pkg; Pkg.add("Clp")' && \
	julia -e 'using Clp' && \
	julia -e 'import Pkg; Pkg.add("JuMP")' && \
	julia -e 'using JuMP' && \
	julia -e 'import Pkg; Pkg.add("MathOptInterface")' && \
	julia -e 'using MathOptInterface'