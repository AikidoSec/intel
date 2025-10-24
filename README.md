[![Intel Github Banner](https://github.com/user-attachments/assets/7a1d7fa4-a861-41fd-8a26-4edfd59da047)](https://intel.aikido.dev/)

# Contributing to the AIKIDO Vulnerability Database

This repository serves as a knowledge base for AIKIDO vulnerabilities. This database is used by [app.aikido.dev](https://app.aikido.dev) and [intel.aikido.dev](https://intel.aikido.dev). New vulnerabilities are published on [X](https://x.com/aikidointel) and distributed via [RSS](http://app.aikido.dev/rss/intel). To contribute a new vulnerability, follow the steps below.

---

## How to Create a Pull Request

### 1. **Fork the Repository**
- Click on the **Fork** button in the top-right corner of this repository to create your copy.

### 2. **Clone the Repository**
- Clone the repository to your local machine.
```bash
git clone https://github.com/<your-username>/intel.git
cd intel
git remote add upstream https://github.com/aikidoSec/intel.git
```

- If you have already forked the repository, update your fork with the upstream repository.
```bash
git remote update
git checkout main
git rebase upstream/main
```

### 3. **Create a New Branch**
- Always branch from `main`.
```bash
git checkout main
git pull origin main
git checkout -b vulnerability-branch-name
```

### 4. **Edit the `new.json` File**
- Navigate to `/input/new.json`.
- Fill in the values of the JSON template with the relevant details for the new vulnerability.
- **Important:** Ensure you follow the structure and required fields of the JSON template. Don't remove/add any fields. Compare against existing files in the `vulnerabilities` directory.
- There’s no need to manually change the file location or file name. An id will automatically be assigned by GitHub Actions & a new file will be created in the `vulnerabilities` directory on pull request merge.

### 5. **Commit Your Changes**
- After editing the file, commit your changes.
```bash
git add input/new.json
git commit -m "Add new AIKIDO vulnerability"
```

### 6. **Push Your Branch**
```bash
git push origin vulnerability-branch-name
```

### 7. **Create a Pull Request (PR)**
1. Go to your repository on GitHub.
2. Click **Compare & pull request** next to your recently pushed branch.
3. Add a meaningful title and description to your PR.
4. Submit the PR to the `main` branch.

### 8. **Review Process**
- Your PR will be validated by automated checks (GitHub Actions).
- Ensure that all checks pass. If any fail, address the issues noted in the logs and push the fixes to your branch.

---

## Guidelines for JSON Fields

Required Fields:
- `package_name`: Name of the affected package.
- `patch_versions`: Array of versions that fix the issue.
- `vulnerable_ranges`: Array of ranges that are vulnerable. If all versions are vulnerable, add string `"*"`.
- `cwe`: Array of related CWE identifiers.
- `tldr`: A short but concise description of the vulnerability.
- `doest_this_affect_me`: A short explanation in which cases the vulnerability affects the user.
- `how_to_fix`: A short explanation on how to fix the vulnerability.
- `vulnerable_to`: The type of attack.
- `related_cve_id`: If a CVE ID already exists (with incorrect information), add the CVE ID here. Otherwise, leave it empty.
- `language`: The programming language of the package (e.g., `js`, `python`, `php`).
- `severity_class`: Severity classification (`LOW`, `MEDIUM`, `HIGH`, `CRITICAL`).
- `aikido_score`: The vulnerability score on a scale of 0-100 (0 is least severe, 100 is most severe).
- `changelog`: The url of the changelog where this vulnerability got fixed.
- `published`: Do not add this field. It will be automatically added by GitHub Actions.
- `last_modified`: Do not add this field. It will be automatically added by GitHub Actions.

Optional Fields:
- `reporter`: Feel free to add your name or company name. Otherwise, leave it empty.
- `package_name_alias`: If the package name is an alias, add the original package name here.
- `package_wildcard_ends_in`: If you want to match partial package names, add the ending here.
- `package_wildcard_contains`: If you want to match partial package names, add the containing string here.
- `extra_specific_non_vulnerable_versions`: If there are specific versions that are not vulnerable, regardles of the version range, add them here.
- `unaffected_distros`: If there are specific distributions that are not vulnerable, regardles of the version range, add them here.
- `simplify_version_if_has_patch_part`: If the version has a patch part in format `9.6_p2-r0+deb9u1`, Aikido will only match on the 9.6 part. Set this to `true` if this is the case.
- `only_for_path_ends_with`: If the vulnerability is only for a specific target path, add the path here.
- `org_name`: In case of a Java package, org_name is required.
- `version_type_hint`: Version type (`semver` or `dpkg`).
- `disable_reachability_analysis`: Package should always be found regardless of not being used in production environment. Set this to `true` if this is the case.


Refer to existing files in the repository for examples.

---

## Important Notes

- **Validation:** The `new.json` file will be checked for correctness by unit tests. Ensure that your JSON complies with the required structure to avoid errors.
- **Merging:** Pull requests cannot be merged if the validation checks fail. Fix any errors before proceeding.
- **Branch Naming:** Use descriptive branch names. There is no strict naming convention.
- **Communication:** Use the PR comments to clarify any doubts or discuss changes.

---

Thank you for contributing to the AIKIDO Vulnerability Database! Your input helps keep the ecosystem secure.
