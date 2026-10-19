# Security in the Wild: An Empirical Analysis of LLM-Powered Applications and Local Inference Frameworks

This repository provides research artifacts associated with the paper “Security in the Wild: An Empirical Analysis of LLM-Powered Applications and Local Inference Frameworks”, published at IEEE/ACM AIware 2025.

The materials support an empirical investigation of security-related characteristics of open-source LLM-powered applications (LPAs) and local inference frameworks (LIFs). They include a GitHub repository collection script, a spreadsheet of security-study data, and a preprint of the paper.

## Repository contents
File |	Description
[`preprint-AIware25.pdf`](preprint-AIware25.pdf) |	Paper preprint describing the study, methodology, and findings.
[`repo_study_summary_security.xlsx`](repo_study_summary_security.xlsx)	| Spreadsheet containing the study's repository-level security data. Consult the spreadsheet and paper for column definitions and interpretation.
[`github_repo_scraper_v3.1.py`](github_repo_scraper_v3.1.py) |	Python script that searches GitHub repositories by LLM-related topics, retrieves selected repository metadata, and heuristically inspects README files for LLM and security-related keywords.
LICENSE |	MIT license for the repository.


## Repository collection script
The provided script uses the GitHub REST API to search for public repositories associated with LLM-related GitHub topics. Its search currently filters for repositories with more than 1,000 stars, orders results by star count, and requests up to 50 results per topic.
For each returned repository, the script collects metadata such as its name, URL, description, primary language, star count, and fork count. It also reads the repository's README.md (trying main, then master) and looks for textual indicators of:
- LLM or model names;
- API-key requirements and shared API keys;
- personal-file upload support;
- caching and logging.
  
The output is a CSV file named repo_study_summary_revision(popular repos).csv. The script can append newly collected entries to that CSV on subsequent runs.
Important limitations: README checks are based on keyword matching. A yes value indicates a matching phrase, not a confirmed feature or security vulnerability; a ? indicates that the script could not establish a value from its checks. Repository descriptions and READMEs can change over time. The script is a data-collection aid and does not itself perform vulnerability scanning or validate the spreadsheet's study conclusions.

## Requirements
- Python 3
- requests
- pandas
- A GitHub personal access token with access to the API endpoints needed for public repository searches

## Install the Python dependencies:
`python -m pip install requests pandas`

## Running the script
1. Obtain a GitHub personal access token and review the API's rate limits.
2. Configure authentication in github_repo_scraper_v3.1.py. The released script uses a GITHUB_TOKEN variable with a placeholder value. Do not commit a real token to a public repository. For safer local use, consider changing the script to read a token from an environment variable.
3. Run:
   `python github_repo_scraper_v3.1.py`
4. Inspect the generated repo_study_summary_revision(popular repos).csv in the current working directory.

The script sleeps briefly between topic queries to reduce request frequency, but GitHub API rate limits may still apply. Re-running it at a later date may produce different results from those used in the published study.

## Study data and reproducibility
The file [`repo_study_summary_security.xlsx`](repo_study_summary_security.xlsx) is provided as a research artifact. For the study design, dataset interpretation, and reported findings, refer to [`preprint-AIware25.pdf`](preprint-AIware25.pdf).

The script and spreadsheet are not guaranteed to be interchangeable outputs: the script writes a CSV with its current search topics and heuristics, while the included XLSX is a separately released study artifact. Reproducing the paper's exact dataset or results may require the methodological decisions and manual analysis described in the paper.

## Citation
If you use this repository or its data in your research, please cite the associated publication:

```Julia Gomezrangel, Young Lee, and Bozhen Liu. “Security in the Wild: An Empirical Analysis of LLM-Powered Applications and Local Inference Frameworks.” 2025 2nd IEEE/ACM International Conference on AI-powered Software (AIware), pp. 149–159, 2025.```

## License
This repository includes an MIT license. If reusing third-party repository data or material, also follow the relevant third-party terms and attribution requirements.

