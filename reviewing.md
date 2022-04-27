# How to review conformance results

## Technical Requirements

1. Verify that the list of files matches the
[expected list](https://github.com/cncf/k8s-conformance/blob/master/instructions.md#contents-of-the-pr).

2. Note the `vX.Y` subdirectory that the PR is in, this is the version of
Kubernetes for which conformance is being claimed, referenced as the
"Conformance Version" from hereon.

3. Verify that the Conformance Version is the current or previous two versions of Kubernetes.

4. Look at `e2e.log`.  Verify that the `major.minor` component of the
`kube-apiserver version:` log and `e2e test version:` both exactly match
the Conformance Version. The patch version does not matter.

5. Verify that the last line of `e2e.log` says "SUCCESS! -- `N` Passed | 0
Failed | 0 Pending | `M` Skipped PASS".  The exact value of `N` and `M` don't
matter as long as we see `0 Failed | 0 Pending`. Also, there should be 0 tests
listed as `Flaked`.

6. Verify that no files outside of the submitted subdirectory are being modified.
For example, if a submission is adding files to `https://github.com/cncf/k8s-conformance/tree/master/v1.18/coyote/`,
ensure that it doesn't change `https://github.com/cncf/k8s-conformance/blob/master/README.md` or
`https://github.com/cncf/k8s-conformance/tree/master/v1.18/roadrunner/`.

## Policy Requirements

1. Confirm that the vendor is currently a
[member](https://www.cncf.io/about/members/) of CNCF. If they are not, request
that they reach out to memberships@cncf.io to become a member in order to
complete their certification. (Companies can alternatively pay a certification
fee equal to the cost of membership if, for whatever reason, they don't wish to
become a CNCF member.) Alternatively, non-profit organizations (including community
distributions like Debian) can certify at no cost.

Review the `PRODUCT.yaml` file, and:

2. Verify that there is a Participation Form on file for the `vendor`, and that
the vendor is in good standing in the program.

3. Verify the product `name` and `website_url` are listed in the
"Qualifying Offerings" section of the vendor's Participation Form, i.e. that
the `name` and `website_url` are listed.

4. Review the `name`. If it contains the word "Kubernetes" in a non-descriptive
fashion, verify that the `name` is listed in "Participant Kubernetes
Combinations" section of the vendor's Participation Form.

If the submission doesn't meet all policy requirements, reply with a message indicating "Signed participation form needed", "Files missing from PR", "Membership in CNCF or confirmation of non-profit status needed", etc.

## Tasks to Complete After Review

1. Update the Kubernetes Distributions & Platforms [spreadsheet](https://docs.google.com/spreadsheets/d/1uF9BoDzzisHSQemXHIKegMhuythuq_GL3N1mlUUK2h0/edit?usp=sharing) to reflect the vendor's certified offering.

2. Add the vendor's information to the [CNCF landscape](https://landscape.cncf.io/grouping=landscape&landscape=certified-kubernetes-distribution,certified-kubernetes-hosted,certified-kubernetes-installer) which also causes them to appear on https://www.cncf.io/certification/software-conformance/ and https://kubernetes.io/partners/#conformance.

3. Add a comment saying "You are now Certified Kubernetes" and merge the PR.
