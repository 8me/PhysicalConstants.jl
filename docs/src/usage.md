## Usage

You can load the package as usual with `using PhysicalConstants` but this module
does not provide anything useful for the end-users.  You most probably want to
directly load the submodule with the dataset you are interested in.  For
example, for CODATA 2018 load `PhysicalConstants.CODATA2018`:

```julia
julia> using PhysicalConstants.CODATA2018

julia> SpeedOfLightInVacuum
Speed of light in vacuum (c_0)
Value                         = 2.99792458e8 m s^-1
Standard uncertainty          = (exact)
Relative standard uncertainty = (exact)
Reference                     = CODATA 2018

julia> NewtonianConstantOfGravitation
Newtonian constant of gravitation (G)
Value                         = 6.6743e-11 m^3 kg^-1 s^-2
Standard uncertainty          = 1.5e-15 m^3 kg^-1 s^-2
Relative standard uncertainty = 2.2e-5
Reference                     = CODATA 2018
```

`SpeedOfLightInVacuum` and `NewtonianConstantOfGravitation` are two of the
`PhysicalConstant`s defined in the `PhysicalConstants.CODATA2018` module, the
full list of available constants is given below.

`PhysicalConstant`s can be readily used in mathematical operations, using by
default their `Float64` value:

```julia
julia> import PhysicalConstants.CODATA2018: c_0, ε_0, μ_0

julia> 2 * ε_0
1.77083756256e-11 F m^-1

julia> ε_0 - 1 / (μ_0 * c_0 ^ 2)
-3.8450973786644646e-25 A^2 s^4 kg^-1 m^-3
```

If you want to use a different precision for the value of the constant, use the
function `float(float_type, constant)`, for example:

```julia
julia> float(Float32, ε_0)
8.854188f-12 F m^-1

julia> float(BigFloat, ε_0)
8.854187812799999999999999999999999999999999999999999999999999999999999999999973e-12 F m^-1

julia> big(ε_0)
8.854187812799999999999999999999999999999999999999999999999999999999999999999973e-12 F m^-1

julia> big(ε_0) - inv(big(μ_0) * big(c_0)^2)
-3.849883307464075736533920296598236938395867709081184624499315166190408485179288e-25 A^2 s^4 kg^-1 m^-3
```

Note that `big(constant)` is an alias for `float(BigFloat, constant)`.

If in addition to units you also want the standard uncertainty associated with
the constant, use `measurement(x)`:

```julia
julia> using Measurements

julia> import PhysicalConstants.CODATA2018: h, ħ

julia> measurement(ħ)
1.0545718176461565e-34 ± 0.0 J s

julia> measurement(Float32, ħ)
1.0545718e-34 ± 0.0 J s

julia> measurement(BigFloat, ħ)
1.054571817646156391262428003302280744722826330020413122421923470598435912734741e-34 ± 0.0 J s

julia> measurement(BigFloat, ħ) / (measurement(BigFloat, h) / (2 * big(pi)))
1.0 ± 0.0
```
