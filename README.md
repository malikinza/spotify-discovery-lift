# Discovery or Cannibalization? A Proxy Study for Spotify's Discovery Mode

Independent project using public Spotify weekly Top 200 chart data (2017-2021). Not affiliated with Spotify. **Work in progress:** data cleaning, event detection and manual review are done; matched controls, lift and the cannibalization check are in progress.

Data: [Kaggle/GitHub mirror](https://github.com/younver/spotify-top-200-dataset). Download it into `spotify-top-200-dataset/` to rerun the notebooks.

## Question
When a late-life streaming spike happens, is it incremental growth for the artist or a reshuffle of the artist's own streams?

## Methodology 
- Cleaned the weekly chart data into one row per track-week (44,200 rows, 221 weeks). Handled a semicolon delimiter, repeated collaborator rows, three date formats and a `'0000'` release-date sentinel.
- Found about 1% of rows with negative weeks-since-release, likely album release dates rather than first single release.
- Detected spikes of 30% or more week over week, with a real previous week, past the first 8 weeks since release, and 8 consecutive weeks of data afterward (146 candidates, 111 after keeping the largest per track).
- Manually reviewed the 15 largest spikes.

## Findings from manual review of top 15 spikes/ candidate events:

1) Most of the top 15 spikes have a plausible non-promotional cause:
    - XXXTENTACION died in June 2018
    - Juice WRLD died in Dec 2019
    - Pop Smoke's posthumous album was released in July 2020, likely pulling his entire catalog up that week
    - Travis Scott Fortnite event happened in April 2020
    - Snowman by Sia is a holiday song, spiked in Dec 2020
    - Bohemian Rhapsody, the 2018 Queen biopic matches the timing of Queen spikes
    - Falling and Streets were likely TikTok trend songs 
    - Popstar spike is 8 weeks after release so it is likely release momentum

2) Three artists (XXXTENTACION, Travis Scott, Queen) account for 9 out of the 15 top spike events. Discovery Mode flags specific songs, so several tracks by one artist spiking in the same week is more consistent with an outside event than with a boost.

3) The data can't separate causes - an algorithmic boost or spike due to external events will look the same in stream count.

## Limitations: 

I manually reviewed only the top 15 spikes, which can be explained by non-promotional causes. Events further down were not manually reviewed and may show other patterns.  

## Conclusion: 

Spike in streams alone cannot show if a track was promoted through Discovery Mode. The flaw in this proxy study is that the "treated" tracks were picked because they spiked regardless of cause. The controls were picked because they did not spike. By design, the treated group therefore contains track spikes due to outside events (deaths, films, TikTok trends), while the controls were chosen for having no such jump. The gap between the groups reflects how they were selected, not only the effect of a boost. A randomized holdout would be a better approach to assess Discovery Mode boost because in a randomized test the boost is assigned before any outcome is known, so outside events affect both groups about equally.

## Next steps: 

A better measure of Discovery Mode promotional effect would be through a randomized holdout experiment. Eligible tracks would be randomly split, and a small subset would receive no boost. Both groups would be measured over the same weeks, and the difference between the groups would be the effect of the Discovery Mode boost.

