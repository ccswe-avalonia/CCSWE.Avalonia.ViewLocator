# Renew or replace Verify

Verify 33+ fails the build without a SponsorCheck license property (SC021). The test csproj claims the
`OpenSource` exemption, which expires `2027-10` (`Verify_SponsorshipExemptionUntil`; 12 months at most).

Immediate.Handlers and Immediate.Apis pin `Verify.XunitV3` 32.0.0; their Dependabot PRs to 33.0.2 are open with
failing checks (Handlers #406, Apis #338).

1. Before `2027-10`, either renew the exemption (new `Verify_SponsorshipExemptionUntil`) or replace Verify.
2. Evaluate replacing it with plain NUnit assertions: a small helper that compares each generated source to the
   existing `Snapshots/*.verified.cs` file. Verify covers 7 tests in `ViewLocatorGeneratorTests` (8 snapshots).
   Replacing it loses auto-accept and diff tooling.
3. If replaced, drop `Verify.NUnit`/`Verify.SourceGenerators` from `src/Directory.Packages.props`, the test
   csproj's exemption properties and `<Using Remove>`, the Verify calls in `ModuleInitializer.cs`, and update the
   Testing section of `CLAUDE.md`.
